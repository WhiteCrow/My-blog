---
layout: post
title: "浅析Ruby里的几个动态方法（二），method_missing方法"
description: ""
category: ["technology"]
tags: ["Ruby"]
---
{% include JB/setup %}


##method_missing 方法是什么？

method_missing方法是Kernel模块（也就是Ruby中最底层模块）的一个方法。 什么时候调用method_missing方法？ 当一个对象调用它并没有定义的方法时，就会调用method_missing方法，听起来有点绕口，让我们来看一个例子:

	obj = Object.new
	obj.send :undefined_method
	=> NoMethodError: undefined method 'undefined_method' for #<Object:0x848d534>

当我们看到 "=> NoMethodError: undefined method 'undefined_method' for #<Object:0x848d534>"这短消息的之前，obj发现它并没有定义undefined_method方法，于是Kernel#method_missing就会抛出一个NoMethodError响应。就像你让一个人去回忆并非发生在他身上的事情时，他搜索了自己的所有记忆，最终回答：“唔，我不记得了。” 如果我们重写某个对象的method_missing方法，它调用并不存在的方法时，就会自动调用method_missing方法,因此我们称它为幽灵方法。当你在死亡笔记上写并不存在的人名时，幽灵就会出来代替那个名字哦。 :) 再举个例子看看：

	def obj.method_missing(method, *args)
	   puts "You called #{method}"
	end
	obj.unknow_method(1,2)

	#=> You called unknow_method

注意，这里一定要写*args这个形式参数，否则调用unknow_method时包含参数的话，会抛出“ArgumentError: wrong number of arguments”的错误。

##method_missing 的作用是什么？

我们再来举个例子看看method_missing 方法的强大之处：

	class Box
	  def method_missing(method, *args, &block)
	      return
	      return
	      super
	  end
	end

这里的super是调用祖先类的同名方法，因为只有Kernel 存在method_missing，它将最后调用Kernel#method_missing 如果说send方法是用于动态调用已经存在的方法，那么method_missing方法则是去动态生成并不存在的方法。那么我们能否动态地改变已存在的方法的内部信息呢？直接执行obj.method;puts "modified";end就行了。 :)

##什么时候使用method_missing方法？

method_missing方法一般用于missing同一类命名模式中的方法。
例子：

	TEMPLATE_CALL_METHODS = [:email_template, :header_menu_msg_template, :recent_activity_msg_template]

	def method_missing(str, *args)
		if TEMPLATE_CALL_METHODS.include? str
	       @viewer = args.shift
	       template = "#{str}_for_#{operation_name}"
	       if respond_to? template
	         send template
	       else
	         send email_template_name
	       end
	     else
	       super
	     end
	end


而不要这样单纯把method_missing方法用作一个防止抛异常方法。错误的用法：

	CATCH_METHODS = [:profile, :email, :full_name]
	def method_missing(str, *args)
		if CATCH_METHODS.include? str
			nil
		else
			super
		end
	end

