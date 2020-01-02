---
layout: page
title: Books
permalink: /books/
---

{% assign book_groups = site.data.books | group_by: 'subject' %}
{% for group in book_groups %}
{{ group.name }}
{% assign sorted-posts = group.items | sort: 'year' %}
<ul>{% for book in sorted-posts %}
	<li>{{book.last}}, {{book.first}}. <a href="https://books.google.com/books?isbn={{book.url}}"><i>{{book.title}}</i></a>. {{book.location}}: {{book.publisher}}. {{book.year}}</li> 
{% endfor %}</ul>
{% endfor %}

