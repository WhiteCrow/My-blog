---
layout: page
title: Welcome My blog!
tagline: Supporting tagline
---
{% include JB/setup %}
<style>
   #disqus_thread{
    	display: none;
   }
   .post-content{
   		margin-top:-20px;
   }
</style>
<div class="row-fluid">
	  {% for post in site.posts %}
	<div class="span6">		    
	    	<a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a>	    	
	    	<li>{{ post.date | date_to_string }}</li> 
	    	<div class="post-content">{{ post.content }}</div>
	</div>
	  {% endfor %}
</div>
