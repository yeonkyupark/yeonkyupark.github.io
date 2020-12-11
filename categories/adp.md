---
layout: category
category: ADP
permalink: "/categories/ADP/"
author_profile: true
---

<!-- 카테고리 추가 S -->
<div class="entries-{{ entries_layout }}">
  {% for category in site.categories %}
    {% if category[0] == page.category %} [ {% endif %} <a href="/categories/{{ category | first }}"> {{ category | first }}</a> {% if category[0] == page.category %} ] {% endif %} &nbsp;
  {% endfor %}    
</div>
<!-- 카테고리 추가 E -->

<h3 class="archive__subtitle">{{ site.data.ui-text[site.locale].recent_posts | default: "Recent Posts" }}</h3>

{% if paginator %}
  {% assign posts = paginator.posts %}
{% else %}
  {% assign posts = site.posts %}
{% endif %}

{% assign entries_layout = page.entries_layout | default: 'list' %}
<div class="entries-{{ entries_layout }}">
  {% for post in site.categories[page.category] %}
    {% include archive-single.html type=entries_layout %}
  {% endfor %}
</div>

{% include paginator.html %}
