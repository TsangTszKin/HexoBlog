---
title: webpack + react + antd + css_modules
date: 2018-11-25 10:27:12
description: '搭建webpack + react + antd + css_modules'
tags: [js, 架构]
categories: '前端'

---

# webpack + react + antd + css_modules
---
###下图是项目目录结构图，红色部分可直接忽略。

![](https://i.imgur.com/GyCWtfh.png)

## 一，初始化项目
###新建项目文件夹，进入目录执行命令

		npm init

可以自动创建一个package.json文件。这是一个标准的npm说明文件，里面蕴含了丰富的信息，包括当前项目的依赖模块，自定义的脚本任务等等。

## 二，安装webpack

	//全局安装
	npm install -g webpack
	//安装到你的项目目录，在本项目中安装Webpack作为依赖包
	npm install --save-dev webpack

## 三，新建模板页面和入口js文件。

### 在根目录下吸纳建src目录，此目录为存放源代码的目录。 进入src目录：

1. 新建index.tmpl.html文件

		<!doctype html>
		<html lang="en">
		
		<head>
		    <meta charset="UTF-8">
		    <meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
		    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
		    <title></title>
		</head>
		
		<body>
		    <div id="root"></div>
		    <!-- <script type="text/javascript" src="./static/layui/layui.all.js"></script> -->
		    <!-- CDN外链的js引入可以写在这里，打包时候把js的整个文件夹copy到输出目录即可 -->
		</body>
		
		</html>

2.新建index.js文件

	import React from 'react';
	import { render } from 'react-dom';
	import "babel-polyfill";
	
	class App extends React.Component {
	    
	    render() {
	        return (
	            <div>
	                //此处可以用一级路由来分拨路由页面。 省略
	            </div>
	        )
	    }
	}
	
	render(<App />, document.getElementById('root'))

## 四，正式使用webpack（一切皆模块）


webpack可以用本地开发服务器作为环境，亦可打包输出后在生产环境上执行。 因此开发环境和生产环境分开配置比较友好。

Webpack有一个不可不说的优点，它把所有的文件都都当做模块处理，JavaScript代码，CSS和fonts以及图片等等通过合适的loader都可以被处理。

webpack提供两个工具处理样式表，css-loader 和 style-loader，二者处理的任务不同，css-loader使你能够使用类似@import 和 url(...)的方法实现 require()的功能,style-loader将所有的计算后的样式加入页面中，二者组合在一起使你能够把样式表嵌入webpack打包后的JS文件中。

### 开发环境

进入根目录

1. 新建webpack.config.js文件。

		const webpack = require('webpack');
		const HtmlWebpackPlugin = require('html-webpack-plugin');//第三方插件，需要安装
		const path = require('path');
		const MiniCssExtractPlugin = require("mini-css-extract-plugin");//第三方插件，需要安装
		
		module.exports = {
		    devtool: 'eval-source-map',//配置source maps，四种之一
		    devServer: {
		        contentBase: "./dist",//本地服务器所加载的页面所在的目录
		        historyApiFallback: true,//不跳转
		        inline: true,//实时刷新
		        hot: true
		    },
		    resolve: {
		        alias: {
		            '@': path.resolve("src")//别名，在js文件访问src文件时候，可以直接用别名@代替
		        },
		        extensions: ['*', '.js', '.jsx', '.json', '.less', '.css']
		    },
		    module: {
		        rules: [
		            {
		                test: /(\.jsx|\.js)$/,
		                use: {
		                    loader: "babel-loader"
		                },
		                exclude: /node_modules/
		            },
		            {
		                test: /\.(png|jpe?g|gif|svg)(\?.*)?$/,
		                loader: 'url-loader',
		                options: {
		                    limit: 10000,
		                    outputPath: "images"
		                }
		            },
		            {
		                test: /(\.less|\.css)$/,
		                use: [//从下往上来选择解析
		                    MiniCssExtractPlugin.loader,
		                    {
		                        loader: 'css-loader',
		                        options: {
		                            importLoaders: 1,
		                            minimize: {
		                                autoprefixer: {
		                                    add: true,
		                                    remove: true,
		                                    browsers: ['last 2 versions'],
		                                },
		                                discardComments: {
		                                    removeAll: true,
		                                },
		                                discardUnused: false,
		                                mergeIdents: false,
		                                reduceIdents: false,
		                                safe: true
		                            }
		                        }
		                    },
		                    {
		                        loader: 'less-loader',
		                        options: {
		                            javascriptEnabled: true
		                        }
		                    }
		                ]
		            }
		        ],
		    },
		    plugins: [
		        new webpack.BannerPlugin('版权所有，翻版必究'),
		        new HtmlWebpackPlugin({//此插件可以配置多入口多页面
		            template: __dirname + "/src/index.tmpl.html",//一个这个插件的实例，并传入相关的参数
		            inject: true,
		            favicon: path.resolve('favicon.ico'),
		            minify: {
		                collapseWhitespace: true,
		            }
		        }),
		        new webpack.HotModuleReplacementPlugin(),//热加载插件
		        new webpack.optimize.OccurrenceOrderPlugin(),//为组件分配ID，通过这个插件webpack可以分析和优先考虑使用最多的模块，并为它们分配最小的ID
		        new webpack.DefinePlugin({
		            'process.env': {
		                'http_env': JSON.stringify(process.env.http_env)
		            }
		        }),
		        new MiniCssExtractPlugin({//压缩JS代码，分离CSS和JS文件
		            filename: 'css/style.css',
		            chunkFilename: 'css/style.[contenthash:5].css'
		        }),
		    ],
		}

2. Babel

Babel用新不用旧，可以

Babel其实是一个编译JavaScript的平台，它可以编译代码帮你达到以下目的：

- 让你能使用最新的JavaScript代码（ES6，ES7...），而不用管新标准是否被当前使用的浏览器完全支持；
- 让你能使用基于JavaScript进行了拓展的语言，比如React的JSX；
- 新建.babelrc文件
 
		 {
		    "presets": [
		      "es2015",
		      "react",
		      [
		        "env",
		        {
		          "modules": false,
		          "useBuiltIns": false,
		          "uglify": true,
		          "targets": {
		            "browsers": ["last 2 versions"]
		          }
		        }
		      ]
		    ],
		    "plugins": [
		      "transform-decorators-legacy",
		      "transform-class-properties",
		      "syntax-dynamic-import",
		      ["transform-runtime",{"polyfill": false}],
		      ["transform-object-rest-spread",{"useBuiltIns": true}],
		      ["import", { "libraryName": "antd", "style": true }]
		    ]
		  }

其中transform-decorators-legacy为装饰器。

Babel其实可以完全在 webpack.config.js 中进行配置，但是考虑到babel具有非常多的配置选项，在单一的webpack.config.js文件中进行配置往往使得这个文件显得太复杂，因此一些开发者支持把babel的配置选项放在一个单独的名为 ".babelrc" 的配置文件中。

3. 同理postcss的配置也可以单独配置，减轻webpack的压力和复杂度。

在根目录新建postcss.config.js

	// postcss.config.js
	module.exports = {
	    plugins: [
	        require('autoprefixer')
	    ]
	}

4.新建webpack.production.config.js文件，比webpack.config.js多了output的配置，少了本地服务器的配置，其余可以不变。

	const webpack = require('webpack');
	const HtmlWebpackPlugin = require('html-webpack-plugin');
	const CleanWebpackPlugin = require("clean-webpack-plugin");
	const path = require('path');
	const MiniCssExtractPlugin = require("mini-css-extract-plugin");
	const CopyWebpackPlugin = require('copy-webpack-plugin');
	
	module.exports = {
	    devtool: "null",
	    entry: __dirname + "/src/index.js", //已多次提及的唯一入口文件
	    output: {
	        path: __dirname + "/dist", //打包后的文件存放的地方
	        filename: "js/bundle.js" //打包后输出文件的文件名
	    },
	    resolve: {
	        alias: {
	            '@': path.resolve("src")
	        },
	        extensions: ['*', '.js', '.jsx', '.json', '.less', '.css']
	    },
	    module: {
	        rules: [
	            {
	                test: /(\.jsx|\.js)$/,
	                use: {
	                    loader: "babel-loader"
	                },
	                exclude: /node_modules/
	            },
	            {
	                test: /\.(png|jpe?g|gif|svg)(\?.*)?$/,
	                loader: 'url-loader',
	                options: {
	                    limit: 10000,
	                    outputPath: "images"
	                }
	            },
	            {
	                test: /(\.less|\.css)$/,
	                use: [
	                    MiniCssExtractPlugin.loader,
	                    {
	                        loader: 'css-loader',
	                        options: {
	                            importLoaders: 1,
	                            minimize: {
	                                autoprefixer: {
	                                    add: true,
	                                    remove: true,
	                                    browsers: ['last 2 versions'],
	                                },
	                                discardComments: {
	                                    removeAll: true,
	                                },
	                                discardUnused: false,
	                                mergeIdents: false,
	                                reduceIdents: false,
	                                safe: true
	                            }
	                        }
	                    },
	                    {
	                        loader: 'less-loader',
	                        options: {
	                            javascriptEnabled: true
	                        }
	                    }
	                ]
	            }
	        ]
	    },
	    plugins: [
	        new CleanWebpackPlugin(['dist', 'build'], { root: __dirname, verbose: true, dry: false }),
	        new webpack.BannerPlugin('版权所有，翻版必究'),
	        new HtmlWebpackPlugin({//此插件可以配置多入口多页面
	            template: __dirname + "/src/index.tmpl.html",//一个这个插件的实例，并传入相关的参数
	            inject: true,
	            favicon: path.resolve('favicon.ico'),
	            minify: {
	                collapseWhitespace: true,
	            }
	        }),
	        new webpack.HotModuleReplacementPlugin(),
	        new webpack.optimize.OccurrenceOrderPlugin(),
	        new webpack.DefinePlugin({
	            'process.env': {
	                'http_env': JSON.stringify(process.env.http_env)
	            }
	        }),
	        new MiniCssExtractPlugin({
	            filename: 'css/style.css',
	            chunkFilename: 'css/style.[contenthash:5].css'
	        }),
	        new CopyWebpackPlugin([{
	            from: path.join(__dirname, 'src/static'),
	            to: path.join(__dirname, 'dist', 'static')
	        }])
	    ]
	}


## 五，修改package.json文件的script字段

### script 是指定义了npm的脚本字段

start：用以开启本地服务器
build： 执行webpack.production.config.js文件

说明：cross-env为跨平台传参 NODE_ENV 和 http_env ，NODE_ENV是要指定开发环境还是生产环境，http_env是自定义的api主机ip地址，为测试环境和生产环境区分开来。支持多生产环境。


	{
	  "name": "zzj-webpack-sample-project",
	  "version": "1.0.0",
	  "description": "这是我的第一个webpack个人搭建",
	  "scripts": {
	    "test": "echo \"Error: no test specified\" && exit 1",
	    "start": "webpack",
	    "server": "cross-env NODE_ENV=development http_env=development webpack-dev-server --open --mode development",
	    "build": "cross-env NODE_ENV=production http_env=production webpack --config ./webpack.production.config.js --progress --mode production"
	  },
	  "main": "main.js",
	  "dependencies": {
	    "@antv/data-set": "^0.9.6",
	    "@antv/g2": "^3.2.7",
	    "antd": "^3.10.8",
	    "axios": "^0.18.0",
	    "babel-plugin-transform-object-assign": "^6.22.0",
	    "babel-polyfill": "^6.26.0",
	    "codemirror": "^5.40.0",
	    "crypto-js": "^3.1.9-1",
	    "extract-text-webpack-plugin": "^4.0.0-beta.0",
	    "immutability-helper": "^2.8.1",
	    "jquery": "^3.3.1",
	    "js-cookie": "^2.2.0",
	    "layui-layer": "^1.0.9",
	    "mobx": "^4.1.0",
	    "mobx-react": "^5.0.0",
	    "object-assign": "^4.1.1",
	    "postcss-flexbugs-fixes": "^4.1.0",
	    "promise": "^8.0.1",
	    "react": "^16.2.0",
	    "react-codemirror": "^1.0.0",
	    "react-codemirror2": "^5.1.0",
	    "react-dnd": "^5.0.0",
	    "react-dnd-html5-backend": "^5.0.1",
	    "react-dom": "^16.2.0",
	    "react-loadable": "^5.3.1",
	    "react-router-dom": "^4.2.2",
	    "viser-react": "^2.3.3",
	    "webpack": "^4.26.0",
	    "whatwg-fetch": "^2.0.4"
	  },
	  "devDependencies": {
	    "autoprefixer": "^9.3.1",
	    "babel-cli": "^6.26.0",
	    "babel-core": "^6.26.0",
	    "babel-loader": "^7.1.3",
	    "babel-plugin-import": "^1.6.6",
	    "babel-plugin-react-transform": "^3.0.0",
	    "babel-plugin-syntax-dynamic-import": "^6.18.0",
	    "babel-plugin-transform-class-properties": "^6.24.1",
	    "babel-plugin-transform-decorators-legacy": "^1.3.4",
	    "babel-plugin-transform-object-rest-spread": "^6.26.0",
	    "babel-plugin-transform-runtime": "^6.23.0",
	    "babel-preset-env": "^1.6.1",
	    "babel-preset-es2015": "^6.24.1",
	    "babel-preset-react": "^6.24.1",
	    "babel-runtime": "^6.26.0",
	    "clean-webpack-plugin": "^1.0.0",
	    "compression": "^1.7.2",
	    "copy-webpack-plugin": "^4.5.1",
	    "cross-env": "^5.1.3",
	    "css-loader": "^0.28.11",
	    "express": "^4.16.2",
	    "file-loader": "^1.1.11",
	    "html-webpack-plugin": "^3.2.0",
	    "less": "^2.7.3",
	    "less-loader": "^4.1.0",
	    "mini-css-extract-plugin": "^0.4.5",
	    "opn": "^5.2.0",
	    "ora": "^2.0.0",
	    "postcss-loader": "^3.0.0",
	    "rimraf": "^2.6.2",
	    "style-loader": "^0.21.0",
	    "url-loader": "^1.0.1",
	    "webpack-cli": "^3.1.1",
	    "webpack-dev-middleware": "^3.1.3",
	    "webpack-dev-server": "^3.1.10",
	    "webpack-hot-middleware": "^2.22.1"
	  },
	  "author": "Tsang",
	  "license": "ISC"
	}
