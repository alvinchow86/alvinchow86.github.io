---
layout: page
title: All posts
permalink: /posts/
---

<div>
{% for post in site.posts %}
    <div>
      <a href="{{ site.baseurl }}{{ post.url }}">
        <h3>{{ post.title }}</h3>

        <!-- <div>
          <p class="post_date">{{ post.date | date: "%B %e, %Y" }}</p>
        </div> -->
      </a>
    </div>
{% endfor %}
</div>
