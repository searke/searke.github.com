---
layout: page
---


# Posts
-----

<ul class="posts">
  {% for post in site.posts %}
    <table class="pure-table">
      <thead>
         <tr><th>
          <span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a>
         </th></tr>
      </thead>
      <tbody>
        <tr><th>
          <p>{{ post.excerpt }}</p>
         </th></tr>
      </tbody>
    </table> 
<br/>

  {% endfor %}
</ul>

