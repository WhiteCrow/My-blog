---
layout: post
title: "Why use Ruby develop DSL"
description: ""
category: ["technology"]
tags: ["Ruby", "DSL"]
---
{% include JB/setup %}

Ruby is great language for develop DSL. Matz said the development
dirction of Ruby is DSL.

Let me see why use Ruby develop DSL ?

1. What are External DSL and Internal DSL ?
   External DSL: Languages that own one parser, such as make, are often called **external DSLs**. 
   Internal DSL: By contrast, Languages that not own paser, that build
by other general-purpose language(GPL).

2. Ruby has Closure named Block that can expediently develop build internal DSL, The standard build language for Ruby (Rake) is just a Ruby library—an internal DSL.

3. Why internal DSL is more good ?
  1) One advantage of an internal DSL is that you can easily fall back
to the underlying GPL whenever you need to do so. However, the syntax of
your internal DSL will be constrained by the syntax of the GPL behind
it.

  2) You can extend internal DSL use GPL.



