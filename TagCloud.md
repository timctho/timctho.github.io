---
layout: page
title: By Tags
---
<ul class="tag-cloud">
{% assign sorted_tags = (site.tags | sort: 0) %}
{% for tag in sorted_tags %}
  <li style="font-size: {{ tag | last | size | times: 100 | divided_by: site.tags.size | plus: 35  }}%">
    <span class="fa-stack fa-sm">
      <i class="fa fa-tags fa-stack-1x"></i>
    </span>
    <a class="tag-wrapper" href="/tags/{{ tag[0] }}">
    <span class="tag-cloud-bbox">{{ tag | first }} ({{ tag | last | size }})</span>
    </a>
  </li>
{% endfor %}
</ul>