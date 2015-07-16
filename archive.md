---
layout: page
title: Archive
---

<!--# All Posts

{% for post in site.posts %}
  * {{ post.date | date: "%B %-d, %Y" }}: [ {{ post.title }} ]({{ post.url }})
{% endfor %}-->

<div class="tag-cloud">
   {% for tag in site.tags %}
      <a href="#posts-tag" id="{{ forloop.index }}" class="__tag" style="margin: 5px">{{ tag[0] }}</a>
      <ul id="list_{{ forloop.index }}" style="display:none;">
         {% for post in tag[1] %}
            <li><a href="{{ post.url }}">{{ post.title }}</a></li>
         {% endfor %}
      </ul>
   {% endfor %}
</div>

<div id ="posts-tags" class="post-list" style="margin: 50px;"></div>

<script type="text/javascript">
   $(function() {
      var minFont = 15.0,
          maxFont = 40.0,
          diffFont = maxFont - minFont,
          size = 0;
       
      {% assign max = 1.0 %}
      {% for tag in site.tags %}
         {% if tag[1].size > max %}
            {% assign max = tag[1].size %}
         {% endif %}
      {% endfor %}
            
      {% for tag in site.tags %}
         size = (Math.log({{ tag[1].size }}) / Math.log({{ max }})) * diffFont + minFont;
         $("#{{ forloop.index }}").css("font-size", size + "px");
      {% endfor %}
      $('.tag-cloud a[class^="__tag"]').click(function() {
         $('.post-list').empty();
         $('#list_' + $(this).attr('id')).each(function() {
            $('.post-list').append('<ul>' + $(this).html() + '</ul>');
         });
      });
   });
</script>

### Articles
{% for post in site.categories['article'] %}
  * {{ post.date | date: "%B %-d, %Y" }}: [ {{ post.title }} ]({{ post.url }})
{% endfor %}

### Links
{% for post in site.categories['link'] %}
  * {{ post.date | date: "%B %-d, %Y" }}: [ {{ post.title }} ]({{ post.url }}) <!--<span class="link-arrow">&rarr;</span>-->
{% endfor %}