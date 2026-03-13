---
title: Blog
layout: default
nav: Blog
nav_order: 1
description: "Practical notes from a .NET developer in Kochi, Kerala — on .NET, Angular, Azure, and AI."
---

<div class="post-header">
  <div class="container">
    <div class="col-lg-8">
      <h1 class="post-title">Blog</h1>
      <p class="post-meta">Practical notes from a developer in Kochi, Kerala — .NET, Angular, Azure, and AI.</p>
    </div>
  </div>
</div>

<div class="container my-5">
  {% if site.posts.size > 0 %}
  <div class="row row-cols-1 row-cols-md-2 row-cols-lg-3 g-4">
    {% for post in site.posts %}
    <div class="col">
      <div class="blog-card h-100">
        <div class="card-body d-flex flex-column">
          <p class="blog-cat mb-1">{{ post.categories | first | default: "Blog" | upcase }}</p>
          <h5 class="mb-2" style="font-size:1rem;font-weight:700;color:#1e293b">{{ post.title }}</h5>
          <p class="text-muted mb-3 flex-grow-1" style="font-size:0.88rem;line-height:1.6">{{ post.excerpt | strip_html | truncate: 140 }}</p>
          <div class="d-flex justify-content-between align-items-center mt-auto">
            <span class="blog-date">{{ post.date | date: "%b %d, %Y" }}</span>
            <a href="{{ post.url | relative_url }}" class="fw-semibold text-decoration-none" style="color:#4f46e5;font-size:0.88rem">Read &rarr;</a>
          </div>
        </div>
      </div>
    </div>
    {% endfor %}
  </div>
  {% else %}
  <p class="text-muted">No posts yet. Check back soon.</p>
  {% endif %}
</div>
