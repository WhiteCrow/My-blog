---
layout: page
title: Welcome My blog!
tagline: Supporting tagline
---
{% include JB/setup %}
<style>
	.post{
		height:400px;
		overflow:hidden;
	}
	li{
		
	}
</style>

<div class="row-fluid"><ul>
	  {% for post in site.posts %}	  
	<li class="post span6">
	    	<a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a>	    	
	    	{{ post.date | date_to_string }}
	    	<div class="post-content">{{ post.content }}</div>		
	</li>
	  {% endfor %}
</ul></div>