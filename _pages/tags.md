---
title: "Browse by Tag"
permalink: /tags/
layout: single
---

{% assign all_tags = "" | split: "" %}
{% for page in site.pages %}
  {% if page.tags %}
    {% for tag in page.tags %}
      {% unless all_tags contains tag %}
        {% assign all_tags = all_tags | push: tag %}
      {% endunless %}
    {% endfor %}
  {% endif %}
{% endfor %}
{% assign all_tags = all_tags | sort %}

<div style="margin-bottom: 24px;">
{% for tag in all_tags %}
  <a href="#{{ tag }}" style="display: inline-block; padding: 4px 10px; margin: 3px; border: 1px solid #ddd; border-radius: 4px; font-size: 13px; text-decoration: none; color: #494e52;">{{ tag }}</a>
{% endfor %}
</div>

{% for tag in all_tags %}
### {{ tag }}
{: #{{ tag }} }

<ul>
{% for page in site.pages %}
  {% if page.tags contains tag %}
  <li><a href="{{ page.url }}">{{ page.title }}</a></li>
  {% endif %}
{% endfor %}
</ul>
{% endfor %}
