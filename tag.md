---
layout: page
permalink: /tags/
title: Tags
---

<div class="tag-cloud">
{% for tag in site.tags %}
    <!-- tag_name 변수 지정: 태그명은 소문자화(slugize) 한다 -->
    {% capture tag_name %}{{tag|first|slugize}}{% endcapture %}
    <!-- font_size 변수 지정: 태그숫자/전체태그숫자 * 100 + 50 -->
    {% capture font_size %}{{tag|last|size| times:100 | divided_by:site.tags.size | plus: 50 }}%{% endcapture %}
    <!-- tag_size 변수 지정-->
    {% capture tag_size %}{{tag|last|size}}{% endcapture %}

    <a href="#{{tag_name}}" onclick="showTag('#{{tag_name}}')">
        {{tag_name}} ({{tag_size}})
    </a>

{% endfor %}
</div>


<div id="archives" style="margin-top:20px;">
{% for tag in site.tags %}

    {% capture tag_name %}{{tag|first|slugize}}{% endcapture %}

    <div class="archive-group" style="" id="{{tag_name}}">

    <h3 id="{{tag_name}}">{{ tag_name }}</h3>

    {% for post in site.tags[tag_name] %}
        <article class="archive-item">
            <h4>
                <!-- click 하여 show/hide 한다 -->
                <a href="{{ root_url }}{{ post.url }}">
                    {{post.title}}
                </a>
            </h4>
        </article>
    {% endfor %}

    </div>
{% endfor %}
</div>

<script src="//ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js"></script>
<script>
    $(document).ready(function init(){
        var url = window.location.href;
        var req = /#([^\s]+)$/.exec(url);

        if(!Array.isArray(req)) {
            return false;
        }
        //var selector = '#' + req.pop();
        var selector = '#dummy-' + req.pop();
        showTag(selector);
    });

    function showTag(selector) {
        $('.archive-group').hide();
        $(selector).show();
    }
</script>