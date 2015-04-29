---
layout: default
---

<div id="home">
    <h1>Welcome</h1>

    <h2>Latest Posts</h2>
    <ul class="posts">
        {% for post in site.posts limit:5 %}
        <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
        {% endfor %}
    </ul>
    
    <p class="rss-subscribe">subscribe <a href="{{ "/feed.xml" | prepend: site.baseurl }}">via RSS</a></p>

    <h2>Tutorial categories</h2>
    <ul>
    {% assign pages_list = site.pages %}
    {% assign group = 'tutorial_top' %}
    </ul>

    <h2>Recommended Open Source Projects</h2>
    <ul class="posts">
        <li><a href="http://projects.spring.io/spring-boot">Spring Boot - Simplifies bootstrapping of Spring applications</a></li>
        <li><a href="http://start.spring.io">Spring Initializr - simple UI to create initial project structure for Spring Boot projects</a></li>
        <li><a href="http://github.com/mojombo/jekyll/">Jekyll:</a> A simple, blog aware, static site generator (used for this site).</li>
    </ul>
</div>


