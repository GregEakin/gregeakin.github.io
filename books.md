---
layout: page
title: Books
permalink: /books/
---
These are a few books that I've found fun to read.

{% assign book_groups = site.data.books | group_by: 'bookcase' %}
{% for group in book_groups %}
{{ group.name }}
{% assign sorted-posts = group.items | sort: 'last', 'first' %}
<ul>{% for book in sorted-posts %}
	<li>{{book.last}}, {{book.first}}. <i><a href="https://books.google.com/books?isbn={{book.isbn}}">{{book.title}}</a></i>. {{book.location}}: {{book.publisher}}. {{book.year}}</li> 
{% endfor %}</ul>
{% endfor %}

