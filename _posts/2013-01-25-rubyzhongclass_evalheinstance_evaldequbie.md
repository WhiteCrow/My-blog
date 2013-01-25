---
layout: post
title: "ruby中class_eval和instance_eval的区别"
description: ""
category: ["technology"]
tags: ["Ruby"]
---
{% include JB/setup %}

（1) C.class_eval "eval_str" 等价于在C中放入eval_str这段代码：class_eval只有类对象(Class Object)才能执行，普通对象没有这个方法。  

（2）obj.instance_eval "eval_str" 等价于class << obj eval_str end，也就是在obj的单例类中放入eval_str这段代码，同时还能访问obj的实例变量！instance_eval对任意实例都可以运行。  

原理简记：  
（1）The Module class defines a method named class_eval . (module_eval is a synonym for class_eval .) ，Class < Module < Object  

（2）The Object class defines a method named instance_eval. ruby中都是对象，所以都可以运行哈。  

示例：

	class Test;end
	Test.class_eval do
		def class_eval_test
			puts "class_eval"
		end
	end
	
	Test.new.class_eval_test
	#=>class_eval

	Test.class_eval do
		puts "class_eval_2"
	end
	#=>class_eval_2

	t = Test.new
	t.instance_eval do
		def instance_eval_test
			puts "instance_eval_test"
		end
	end

	t.instance_eval_test
	#=>instance_eval_test

	Test.instance_eval_test
	#=>NoMethodError: undefined method `instance_eval_test' for #<Class:0x00000002a84df8>::Test
	
