---
title: java
date: 2016-11-04 13:49:57
tags: 'java'
categories: '后端'
description: 'java的一些工具类'

---

##判断当天为星期几
	
	public int getWeek() {

	    SimpleDateFormat format = new SimpleDateFormat("yyyy-MM-dd");
	    Calendar c = Calendar.getInstance();
	    Date date = new Date();
	    c.setTime(date);
	
	    String day = format.format(date);
		int currentdayForWeek = 0;

		if (c.get(Calendar.DAY_OF_WEEK) == 1) {
	        currentdayForWeek = 7;
	    } else {
	        currentdayForWeek = c.get(Calendar.DAY_OF_WEEK) - 1;
	    }
		return currentdayForWeek;
	}


##对List中的某个属性进行排序

###int 类型排序
	如List<Activities>降序

	Collections.sort(activities, new Comparator(){
		@Override
		public int compare(Object o1, Object o2) {
		     Activities act1 =(Activities)o1;
		     Activities act2 =(Activities)o2;
			if(act1.getId()<act2.getId()){
			    return 1;
			}else if(act1.getId()==act2.getId()){
			    return 0;
			}else{
			    return -1;
			}
		}
	});
###String 类型排序（字母）
	如List<Student> studentList升序

	Collections.sort(studentList, new Comparator(){
		@Override
		public int compare(Object o1, Object o2) {
		    Student stu1 = (Student)o1;
		    Student stu2 = (Student)o2;
			return stu1.getName().compareTo(stu2.getName());
		}
	});

##java URL编码解码
	URLEncoder.encode("这里是String字符串", "utf-8")
	URLDecoder.decode("这里是String字符串", "utf-8")

##计算两个日期之间相差的天数
	
	/**
	 * 计算两个日期之间相差的天数
	 * @param smdate 较小的时间
	 * @param bdate  较大的时间
	 * @return 相差天数
	 * @throws ParseException
	 */
	public static int daysBetween(Date smdate,Date bdate) throws ParseException
	{
	    SimpleDateFormat sdf=new SimpleDateFormat("yyyy-MM-dd");
	    smdate=sdf.parse(sdf.format(smdate));
	    bdate=sdf.parse(sdf.format(bdate));
	    Calendar cal = Calendar.getInstance();
	    cal.setTime(smdate);
	    long time1 = cal.getTimeInMillis();
	    cal.setTime(bdate);
	    long time2 = cal.getTimeInMillis();
	    long between_days=(time2-time1)/(1000*3600*24);
	
	    return Integer.parseInt(String.valueOf(between_days));
	}

##java Date 
年月日时分秒 对应于数据库 datetime