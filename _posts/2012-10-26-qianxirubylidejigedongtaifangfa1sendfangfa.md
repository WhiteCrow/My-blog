---
layout: post
title: "浅析Ruby里的几个动态方法（一），send方法"
description: ""
category: ["technology"]
tags: ["Ruby"]
---
{% include JB/setup %}

动态方法，是去控制静态方法的方法，让静态方法的方法名和方法的内容会根据参数的变化而变化，简而言之，他使方法成为了一个变量。让我们通过一个多态实例，来理解一下最简单的动态方法send。

所谓多态就是把不同种类的东西当作相同的东西来处理。比如我要打开三个箱子，打开的方法都不同，如果发出同样打开箱子的命令，3个人都会以自己的方法来打开箱子。在编程中，“打开箱子”的命令，我们称之为消息；而打开不同箱子的具体操作，我们称之为方法。

示范程序：

	def box1.open
	  puts("open box")
	end

	def box2.open
	     puts("open lock and open box")
	end

	def box3.open
	      puts("It's a open box")
	end

这里设置了box1、box2、box3三个方法，但是当我们预先并不知道要调用哪一个box方法时，就会写出类似下列这样的when……case表达式，在面向对象中这种写法是较为丑陋的：

	def open(num)
	  case num
	  when 1;puts("open box")
	  when 2;puts("open lock and open box")
	  when 3;puts("It's a open box")
	  when 4;puts("I can't open box")
	  when 5;puts("Oh shit box!")
	  end
	end

	box.open(1)

如果我们加上使用send方法，就可以将case……when给解藕，使程序降低了耦合性，增加了拓展性。send方法的作用是将一个方法传递给对象，例：

	1.send(:+,2)
	>3

下面的例子是解藕def open(num)

	class Box
	  def open_1
	      puts "open box"
	  end

	  def open_2
	      puts "open lock and open box"
	  end

	  def open_3
	      puts "It's a open box"
	  end

	  def open_4
	      puts "I can't open box"
	  end

	  def open_5
	      puts "Oh shit box!"
	  end  
	end

	box = Box.new

	box.send("open_#{num}")

这样，将num作为参数，用的open_num方法。 但这里需要注意的是，send方法太过强大，可以调用任何方法，包括私有方法，使用public_send方法将能够尊重方法接受者的隐私权，可以用它来代替send方法。

###send方法的函数式用法  
最近看了这篇[四个程序员的一天](http://justjavac.iteye.com/blog/170076)觉得很有意思，照着写了个ruby的函数式写法：

	def foo(op, a, b)
		a.send(op, b)
	end
