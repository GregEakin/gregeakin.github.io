---
layout: page
title: Books
permalink: /books/
---
These are a few books that I've found fun to read.

{% assign book_groups = site.data.books | group_by: 'bookcase' %}
{% for group in book_groups %}
{{ group.name }}
{% assign sorted-posts = group.items | sort: 'name', 'last' %}
<ul>{% for book in sorted-posts %}
	<li>{{book.name}}. <i><a href="https://www.amazon.com/s?k={{book.isbn}}">{{book.title}}</a></i>. {{book.location}}: {{book.publisher}}. {{book.year}}</li> 
{% endfor %}</ul>
{% endfor %}

