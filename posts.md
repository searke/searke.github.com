---
layout: page
---


### Posts

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  
  <p>{{ post.excerpt }}</p>
<br/>

  {% endfor %}
</ul>

