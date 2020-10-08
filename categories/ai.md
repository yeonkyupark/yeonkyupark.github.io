---
layout: archive
category: A.I.
author_profile: true
---
<div class="entries-{{ entries_layout }}" align="right">
  {% for category in site.categories %}
    {% if category[0] == page.category %} <u><b> {% endif %} <a href="/categories/{{ category | first }}"> {{ category | first }}</a> {% if category[0] == page.category %} </b></u> {% endif %} &nbsp;&nbsp;
  {% endfor %}
</div>

<h3 class="archive__subtitle">{{ site.data.ui-text[site.locale].recent_posts | default: "Recent Posts" }}</h3>

{% assign entries_layout = page.entries_layout | default: 'list' %}
<div class="entries-{{ entries_layout }}">
  {% for post in site.categories[page.category] %}
    {% include archive-single.html type=entries_layout %}
  {% endfor %}
</div>

{% include paginator.html %}
