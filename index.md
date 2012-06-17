---
layout: page
title: Most Recent
tagline: The latest posts
---
{% include JB/setup %}
#[{{site.posts[0].title}}]({{site.posts[0].url}})
- - -
{{site.posts[0].content}}
- - -
##Latest Posts
{% for post in site.posts offset:1 limit:3 %}


<div class="alert alert-disabled">
	<a class="close" href="#">{{ post.date | date: "%b %e, %Y"}}</a>
	<h3 class="alert-heading"><a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a> <small>in {{post.categories}}</small></h3>
	<p>{{ post.content | strip_html | truncatewords:125}}</p>
	<hr class="thin">
	<div class="alert-actions">
	<span class="tag_box">{% for tag in post.tags %} <a href="{{ BASE_PATH }}{{ site.JB.tags_path }}#{{ tag }}-ref">{{ tag }}</a> {% endfor %}</span>
	<a class="btn btn-info btn-mini" style="float: right;" href="{{ BASE_PATH }}{{ post.url }}">Read More</a>
	</div>
</div>
{% endfor %}