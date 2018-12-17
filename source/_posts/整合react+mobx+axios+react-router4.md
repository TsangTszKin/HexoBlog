---
title: 整合react + mobx + axios + react-router4
date: 2018-12-01 10:27:12
description: '一步步整个整合react + mobx + axios + react-router4'
tags: [js, 架构]
categories: '前端'

---

# react + mobx + axios + react-router4

----------

![](https://i.imgur.com/SrLftUC.png)

## 一，定义axios的api接口
### aService.js

	import axios from 'axios';
	const errorHandler = error => {
	    console.log("出错信息如下");
	    console.log(error);
	}
	const host = 'http://www.example.com';

	export default {
		getList(){
			return axios.get(`${host}/api/XXX`).catch(errorHandler);//get, post, put, delete方法都有
		},
		getDetail(id) {
			return axios.get(`${host}/api/XXX?id=${id}`).catch(errorHandler);
		}
	}
	//bService.js 同理

<br />

## 二，定义mobx数据仓库
原则上一个页面级组件及其的子组件都公用一个实例化的数据仓库
### AStore.js

	import { observable, action, toJS, computed } from 'mobx';
	import aService from 'aService';
	
	/**
	 * A 自己的store
	 * 在 页面级 通过 Provider 渗透到所有子组件。
	 * 在子组件内用 @inject('store')，将 store 注入到自己的 props 上。
	 */
	class Store {
		constructor() {
	        this.getListForApi = this.getListForApi.bind(this);
	    }

	    @observable list = []; //被观察的属性数据
		@computed get getList(){ return toJS(this.list) } //get方法, 把observer类型转为js的类型返回
		@action.bound setList(value) { this.list = value; } //set方法
		
		getListForApi(){
			aService.getList().then(this.getListForApiCallBack);
		}
		@action.bound getListForApiCallBack(res){
			//这里的api回调必须这样分开写才可以被观察到
			//这里调用api，拿到后台返回的数据后，把list赋值
		}
	}
	
	export default new Store
	// 导出一个new的Store，确保渗透的数据仓库都用同一份数据，同一个实例

### ADetailStore.js

	import { observable, action, toJS, computed } from 'mobx';
	import aService from 'aService';

	class Store {
		constructor() {
	        this.getDetailForApi = this.getDetailForApi.bind(this);
	    }
		
		@observable id = '';
		@computed get getId(){ return toJS(this.id) } //get方法
		@action.bound setId(value) { this.id = value; } //set方法

	    @observable info = {
			name: '',
			code: '',
			get getName(){ return toJS(this.name) },
			setName(value){ this.name = value; },
			get getCode(){ return toJS(this.code) },
			setCode(value){ this.code = value; }
		}
		
		getDetailForApi(){
			aService.getDetail(this.getId).then(this.getDetailForApi);
		}
		@action.bound getDetailForApiCallBack(res){
			//todo
		}
	}
	
	export default new Store

<br />
## 三，定义页面级组件
### A.js

	import React from 'react';
	import PropTypes form 'prop-types';
	import { observer, Provider } from 'mobx-react';
	import store from 'AStore';
	import { withRouter } from 'react-router-dom';

	@withRouter	//可获取路由信息并且有改变路由的权限
	class A extends React.Component{
		constructor(props) {
	        super(props);
	    }
		render(){
			return (
				<div>
					<ul>
						{store.getList.map((item, i)=>
							<li key={i}>{item.name}</li>
						)}	//获取store的数据并且循环渲染
					</ul>
					<button
						onClick={()=>this.props.history.push('/a/123')} //跳转到A的详情页面并且附带参数值123
					></buton>
				</div>
			)
		}
	}
	A.propTypes = {
		name: PropTypes.string.isRequired
	}
	A.defaultProps = {name: ''}
	export default A; 
	//B同理
	//用了mobx的数据仓库可以用全局的数据来控制，用引进的store做数据仓库propTypes和defaultProps可不写

### ADetail.js

	import React from 'react';
	import PropTypes form 'prop-types';
	import { observer, Provider } from 'mobx-react';
	import store from 'ADetailStore';
	import { withRouter } from 'react-router-dom';
	
	@withRouter
	class ADetail extends React.Component{
		constructor(props) {
	        super(props);
	    }
		componentDidMount() {
        	store.getDetailForApi();
    	}
		render(){
			return (
				<Provider store={store}>
					<div>
						ID参数值 是｛this.props.match.params.id｝
						//这里可以显示和调用store的方法和数据 
					</div>
				</Provider>
			)
		}
	}
	export default ADetail;
	//BDetail同理

### ADetailComponent.js

	import React from 'react';
	import { observer, inject } from 'mobx-react';
	
	@inject('store')	//inject写在observer之前
	@observer			//检测页面随着检测的数据变化而发生变化
	class ADetailComponent extends React.Component{
		constructor(props) {
	        super(props);
	    }
		
		render(){
			return (
				<div >
					名称 ： {this.props.store.info.getName}
					//这里可以显示和调用父层组件（不限）ADetail渗透进来的store的方法和数据 
				</div>
			)
		}
	}
	export default ADetailComponent;

### Error404.js

	import React from 'react';
	
	class Error404 extends React.Component{
		
		render(){
			return (
				<div >
					404页面
				</div>
			)
		}
	}
	export default Error404;

## 四，定义路由配置文件 
### routersConfig.js
	//配置不用写登录页和404这种特殊页面，只写菜单导航页即可
	import A from 'A';
	import ADetail from 'ADetail';
	import B from 'B';
	import BDetail from 'BDetail';

	export default
	 [{
	        'path': '/a',
	        'component': A,
	        'meta': {} //这里是自定义的信息。可写可不写
	 },{
	        'path': '/a/:id', //这里是id是必传的参数如 /a/123
	        'component': ADetail
	 },{
	        'path': '/b',
	        'component': B
	 },{
	        'path': '/b/:id?', //这里是id是非必传的参数如 /a/123 或者 /a 都不会报错
	        'component': BDetail,
	 },]

<br />

## 五，定义路由入口文件
### 一级路由index.js

	import React, { Component } from 'react';
	import { Route, Switch, withRouter } from 'react-router-dom';
	import LoginPage from 'LoginPage';
	import MainPage from 'MainPage';
	
	@withRouter
	class Index extends Component {
		constructor(props) {
	        super(props);
	    }
		componentWillMount() {
			//判断是否已登录
		}
		componentWillReceiveProps() {
			//判断是否已登录
		}
		render (){
			return (
				<div>
					<Switch>
	                    <Route path="/login" component={LoginPage} />
	                    <Route path='/' component={MainPage} />
	                </Switch>
				</div>
			)
		}
	}
	export default Index
<br />

### 二级路由MainPage.js

	import React, { Component } from 'react';
	import { Route, Switch, withRouter } from 'react-router-dom';
	import routerConfig from 'routerConfig'; //导入路由配置文件作遍历
	import Error404 from 'Error404';

	class MainPage extends Component {
		constructor(props) {
	        super(props);
	    }
		render (){
			return (
				<div>
					<NavComponent />
	                <MainContent />
				</div>
			)
		}
	}
	
	//导航组件
	class NavComponent extends Component {
		render (){
			return (
				<div>
				</div>
			)
		}
	}

	//页面主组件
	@withRouter
	class MainContent extends Component {
		render (){
			return (
				<div>
					<Switch>
                         {routerConfig.map((item, i) =>
                             <Route key={i} path={item.path} exact render={props =>
                                 <item.component collapsed={this.props.collapsed} changeCollapsed=	{this.props.changeCollapsed} meta={item.meta} />
                                } >
                             </Route>
                         )}
                          <Route exact component={Error404}></Route>
                    </Switch>
				</div>
			)
		}
	}
	export default MainPage

# 完成