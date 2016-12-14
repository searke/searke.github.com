---
layout: page
---


# Posts
-----

<div>
  {% for post in site.posts %}
    <section class="post">
	<header class="post-header">
	<h2 class="post-title">
	 <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a>
	</h2>
	<p class="post-date">
		{{ post.date | date_to_string }}
	</p>
	</header>
	<div class="post-description">
		{{ post.excerpt }}
	<p>
	</p>
	</div>
     </section>


<br/>

  {% endfor %}
</div>
