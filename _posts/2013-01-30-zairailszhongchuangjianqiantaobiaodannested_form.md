---
layout: post
title: "在rails中创建嵌套表单(nested form)"
description: ""
category: ["technology"]
tags: ["blog", "jekyll", "note"]
---
{% include JB/setup %}

首先处理需要嵌套表单相关的model，在这里我们是用tile来嵌套attachment，所以model的代码分别是:

	class Tile < ActiveRecord::Base
	  has_many :attachments, :as => :attachable, :dependent => :destroy
	  accepts_nested_attributes_for :attachments, :allow_destroy => true
	  .....
	end

	class Attachment < ActiveRecord::Base
	  belongs_to :attachable, :polymorphic => true
	  .....
	end

这里accepts_nested_attributes_for的作用是允许tile去嵌套attachment的属性，接下来我们看如何在view中代码：

	<%= form_for @tile do |f| %>
	  ....
	  ##@tile本身的一些属性
	  f.fields_for :attachments do |builder|
	  	##这里注意，使用了fields创建了一个和attachment相关的fileds
		<% unless builder.object.new_record? %>
  		  <p id = "<%= builder.object.id %>">
			<%= image_tag file_type_icon_path(builder.object.file_type) %>
			<%= builder.object.file_name %>
			<%= check_box :_destroy, style: 'display:none' %>
		  </p>
		<% end %>
	<% end %>

需要注意的是，在这段代码中，除了自己创建的一部分fields外，fields_for还会创建一个隐藏field用于处理每一个attachment，他的HTML代码类似这样：<input id="action_tile_attachments_attributes_0_id" name="action_tile[attachments_attributes][0][id]" type="hidden" value="53" />


代码中的builder.check_box :_destroy 被勾选后会自动生成一些参数给params[:tile]去删除attachments参数类似a于"tile" => {"attachments_attributes"=>{"0"=>{"_destroy"=>"1", "id"=>"54"}}。
当参数传递给tile.update_attributes后就会自动删除被勾选的attribute了。这就是在rails中构建嵌套表单的方式了。
