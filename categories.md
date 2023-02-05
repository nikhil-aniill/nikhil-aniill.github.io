---
title: /categories
layout: page
permalink: /categories
---
<h1> Categories </h1>

{%- for post in site.posts -%}
	<ul>
	{% case post.category %}
	  {% when 'Assembly' %}
		<h2>{{post.category}}</h2>
		<li>
		<a href="{{ post.url | relative_url }}">{{ post.title | escape }}</a>
		</li>
	  {% when 'DFIR' %}
	  	<h2>{{post.category}}</h2>
		<li>
		<a href="{{ post.url | relative_url }}">{{ post.title | escape }}</a>
		</li>
	{% endcase %}
{%- endfor -%}