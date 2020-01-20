---
layout: default
title: Home
pagination: 
  enabled: true
---
<!-- Tech Selector
================================================== -->
<div class="filterbutton">
  <a href="/lowtech"
    >low tech</a>
  <a href="/midtech"
    >medium tech</a>
  <a href="/hightech"
    >high tech</a>
  <a class="btnactive" href="/">Alle</a>
</div>

{% if page.url == "/" %}
<!-- Featured
================================================== -->
<section class="featured-posts">
    <div class="section-title">
        <h2><span>Featured</span></h2>
    </div>
    <div class="row">

    {% for post in site.posts %}

        {% if post.featured == true %}

            {% include featuredbox.html %}

        {% endif %}

    {% endfor %}

    </div>
</section>

{% endif %}

<!-- Posts Index
================================================== -->
<section class="recent-posts">

    <div class="section-title">

        <h2><span>Alle Activiteiten</span></h2>

    </div>

    <div class="row listrecent">

        {% for post in paginator.posts %}

        {% include postbox.html %}

        {% endfor %}

    </div>

</section>

<!-- Pagination
================================================== -->
<div class="bottompagination">
<div class="pointerup"><i class="fa fa-caret-up"></i></div>
<span class="navigation" role="navigation">

<!-- Fix pagination bug https://github.com/sverrirs/jekyll-paginate-v2/issues/140 -->
    
<!-- Set the trail for every page -->
{% assign trail_begin = paginator.page | minus: site.pagination.trail.before %}
{% assign trail_end = paginator.page | plus: site.pagination.trail.after %}
<!-- In case there are not enough pages before the current one -->
{% if trail_begin < 1 %}
    {% assign trail_begin = 1 %}
{% endif %}
<!-- In case there are not enough pages after the current one -->
{% if trail_end > paginator.total_pages %}
    {% assign trail_end = paginator.total_pages %}
{% endif %}

  
<div class="pagination">
  {% if paginator.total_pages > 1 %}
    
    {% if paginator.previous_page %}
    
      <a href="{{ paginator.previous_page_path | prepend: site.baseurl }}">&laquo;</a>
    
    {% endif %}
    
    {% if paginator.page_trail %}
      {% for trail in paginator.page_trail %}
        <a href="{{ trail.path | prepend: site.baseurl }}" title="{{trail.title}}" {% if page.url == trail.path %}class="active"{% endif %}>{{ trail.num }}</a>
      {% endfor %}
    {% else %}
      <!-- Fix pagination bug https://github.com/sverrirs/jekyll-paginate-v2/issues/140 -->
      {% for pagenum in (trail_begin..trail_end) %}
        {% if pagenum == 1 %}
          <a href="/" title="{{trail.title}}" {% if paginator.page == pagenum %}class="active"{% endif %}>{{ pagenum }}</a>
        {% else % }
          {% assign pagenumpath = "page/" | append: pagenum %}
          <a href="/page/{{ pagenum }}" title="{{trail.title}}" {% if paginator.page == pagenum %}class="active"{% endif %}>{{ pagenum }}</a>
        {% endif %}
      {% endfor %}
    {% endif %}
    
    {% if paginator.next_page %}
      <a href="{{ paginator.next_page_path | prepend: site.baseurl }}">&raquo;</a>
    {% endif %}
    
 {% endif %}
</div>  
</span>
</div>
