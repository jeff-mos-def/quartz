---
title: tags
permalink: /tags
format: list
description: Postings by associated tag for quick filtering.
order: 10
---

<div class="tags" style="margin-bottom: 20px;">
  <!-- Collect all tags -->
  {% assign all_tags = '' | split: ',' %}
  {% for note in site.notes %}
    {% if note.path contains '100_Notes' %}
      {% for tag in note.tags %}
        {% unless all_tags contains tag %}
          {% assign all_tags = all_tags | push: tag %}
        {% endunless %}
      {% endfor %}
    {% endif %}
  {% endfor %}
  {% assign sorted_tags = all_tags | sort %}

  <!-- Display all tags as links with updated styling -->
  {% for tag in sorted_tags %}
    <span style="margin-right: 10px;">
      <a href="#{{ tag | slugify }}" style="text-decoration: none; padding: 5px; background-color: transparent; display: inline-block; margin-bottom: 5px; color: #FAFAFC;">
        {{ tag | capitalize }}
      </a>
    </span>
  {% endfor %}
</div>



<div class="tagged-notes">
  <!-- Display notes for each tag -->
  {% for tag in sorted_tags %}
    <div id="{{ tag | slugify }}" class="tag-section">
      <h2>{{ tag | capitalize }}</h2>
      {% for note in site.notes %}
        {% if note.path contains '100_Notes' and note.tags contains tag %}
          <h3>
            <a href="{{ site.baseurl }}{{ note.url }}">{{ note.title }}</a>
          </h3>
          <p>{{ note.excerpt | strip_html | truncatewords: 20 }}</p>
        {% endif %}
      {% endfor %}
    </div>
  {% endfor %}
</div>
