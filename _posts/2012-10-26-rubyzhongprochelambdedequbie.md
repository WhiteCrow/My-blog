---
layout: post
title: "Ruby中Proc和lambda的区别"
description: ""
category: ["technology"]
tags: ["Ruby"]
---
{% include JB/setup %}

Proc和lambda有两个区别，一个是return的作用范围，另一个是参数的处理方式。我们来用几个例子解释一下：

	def foo
	  f = Proc.new{|a,b| return [a,b]}
	  puts f.call(1)
	  return "I'm not display"
	end

	def bar
	  b = lambda{|a,b| return [a,b] }
	  puts b.call(1,2)
	  return "I will display"
	end

	foo
	# => [1, nil]
	bar
	# 1 
	# 2
	#=> "I will display" 

##参数处理

我们可以看到，假设Proc和lambda两者都定义了2个参数，但在实际调用时，只传一个的话，lambda 会报错，Proc 将缺失的参数设为 nil，然后正常调用。 f.call(1)时，得到的是[1,nil] 而b.call(1)时，则会报错：ArgumentError: wrong number of arguments (1 for 2)

##retunr范围

在一个方法内使用Proc/lambda时，在bar方法中，如果Proc内包含了return，则执行到Proc内的return就不再往下执行。换言之，proc的return是作用于整个方法的。 而在bar方法中，lambda的return将不会影响方法的继续执行，lambda的return仅仅作用于代码块的内部。