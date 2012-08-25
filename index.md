---
layout: page
title: Welcome My blog!
tagline: Supporting tagline
---
{% include JB/setup %}
<style>
	.post-content{
		height:350px;
		overflow:hidden;		
	}
	.post{
		float:left;	
	}
	.post-content{		
		color:black;
	}
	.post a:hover{
		display: block;
		text-decoration:none;        
	}
	#cover{
        filter:alpha(opacity=40);
        -moz-opacity: 0.4;
        opacity: 0.4;
        background-color:#fff;
        z-index:5; 
	}
</style>

<div class="row-fluid">
	{% for post in site.posts %}
	 <div class="span4">
			<div class="post" id="no" onmouseover = "$(this).attr('id','cover')" onmouseout ="$(this).attr('id','no')">
				<a href="{{ BASE_PATH }}{{ post.url }}">
			    	{{ post.title }}<br>
			    	>> {{ post.date | date_to_string }}
			    	<div class="post-content">{{ post.content }}</div>
			    </a>
			    <br>
			</div>
	</div>	
	{% endfor %}
</div>