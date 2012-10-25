---
layout: page
title: Welcome My blog!
tagline: Supporting tagline
---
{% include JB/setup %}

<style>
	.post-content{		
		
	}
	.post{
		height:350px;		
		overflow:hidden;		
		margin-bottom:35px;		
	}
	.post-content{		
		color:black;
	}
	.post a:hover{
		display: block;
		text-decoration:none;        
	}
	#cover{
        /*filter:alpha(opacity=40);
        -moz-opacity: 0.4;
        opacity: 0.4;
        background-color:#fff;
        z-index:5; */
	}
</style>

<div class="row-fluid">
	{% for post in site.posts %}
	 <div class="span5">
			<div class="post" id="no" onmouseover = "$(this).attr('id','cover')" onmouseout ="$(this).attr('id','no')">
				<a href="{{ BASE_PATH }}{{ post.url }}">
			    	{{ post.title }}
			    	<li>{{ post.date | date_to_string }}</li>
			    	<br>
			    	<div class="post-content">{{ post.content }}</div>
			    </a>			    
			</div>
	</div>	
	{% endfor %}
</div>