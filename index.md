---
layout: page
title: Welcome My blog!
tagline: What about my life
---
{% include JB/setup %}

<style>
	/*.post-content{		
		
	}
	.post{
		height:350px;
		text-overflow: ellipsis;
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
        filter:alpha(opacity=70);
        -moz-opacity: 0.7;
        opacity: 0.7;
        background-color:blue;
        z-index:5; 
	}*/
	#cate{
		float: left;
		margin:10px;		
		margin-right:30px;
	}
	#about{
		margin:10px;		
	}
	#social{		
		margin:10px;		
	}
	#social h2{		
		margin-bottom:5px;		
	}
</style>

<a href="/archive.html"><img src="{{ ASSET_PATH }}/dinky/images/index/index.png" width="940px" /></a>

<div id="cate">
{% for category in site.categories %} 
  <h2 id="{{ category[0] }}-ref">{{ category[0] | join: "/" }}</h2>
  <ul>
    {% assign pages_list = category[1] %}  
    {% include JB/pages_list %}
  </ul>
{% endfor %}
</div>
<div id="about">
	<h2>About me</h2>
Hi, my name is LiuSihao. This is my personal blog that meant to share with you those common technical problems and My picture in your work or your life, especially in web related development. I am mainly working on Ruby on Rails related projects half years..I like comic, draw, read and write novels, too.
</div>

<div id="social">
	<h2>Find me</h2>
	<a href=""><img src="{{ ASSET_PATH }}/dinky/images/about/douban.gif"/></a>
	<a href=""><img src="{{ ASSET_PATH }}/dinky/images/about/github.jpg" style= "width:50px;height:50px;"/></a>
	<a href=""><img src="{{ ASSET_PATH }}/dinky/images/about/sinaminiblog.gif"/></a>
	<a href=""><img src="{{ ASSET_PATH }}/dinky/images/about/twitter.gif"/></a>
</div>
<!-- 
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
</div> -->