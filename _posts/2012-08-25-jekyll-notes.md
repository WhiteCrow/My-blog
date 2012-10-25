---
layout: post
title: "Jekyll notes"
description: ""
category: [technology]
tags: [blog],[jekyll],[note]
---
{% include JB/setup %}

###Document:[jekyllbootstrap](http://jekyllbootstrap.com/)		
<br>
1. Preview:
>jekyll --server  
<br>
2. Create a Post:
>rake post title="Hello World"  
<br>
3. Create a Page:
>rake page name="about.md"  
>rake page name="pages/about.md"  
>rake page name="page/about" (this will create the file: ./pages/about/index.html)  
<br>
4. Customize Themes:
>modify "./_includes/themes/THE-NAME" folder
>modify "./index.md"
5. deploy:
>git commit -m "Add new content"
