---
layout: post
title: "Ruby里yeild和block的用法"
description: ""
category: ["technology"]
tags: ["Ruby"]
---
{% include JB/setup %}
---
##Ruby里yeild和&block的用法
<br>
###例子：

	class Box
	   def do(who,kind,&block)
	     "#{who} #{yield} #{kind} #{self.class}"
	   end
	end

	#这个方法里，&block作为一个代码块参数，被yield所调用。
	#注意这里的&block只能作为最后一个参数，否则会报错。

	box = Box.new
	box.do("I","iron"){ return "open" }
	#=> "I open iron Box"

	box.do("She","wooden"){ "kick" }
	#=> "She kick wooden Box"

###让我们来做一个改进版：

	class People
	  def initialize(name)
	      @name = name
	  end
	  attr_reader :name
	end

	class Box
	  def initialize(kind)
	      @kind = kind
	  end
	  def is_done(who, &block)
	      if who.class == People
	          "#{@kind} #{self.class} #{yield} by #{who.name}"
	      else
	          "#{who} not a people"
	      end
	  end
	end

	#因为kind并非is_done的固有属性，而是Box的属性，所以它是作为一个参数传进box对象
	#而is_done则是作为Box的被动语态，所以is_done方法属于box

	daniel = new people("Daniel")
	box = Box.new("wooden")

	box.is_done(daniel){ "open" }
	#=> "wooden Box open by Daniel"

	box.is_done("bird"){ "open" }
	#=> "bird not a people" 