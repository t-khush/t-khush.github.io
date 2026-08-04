---
layout: default
title:
description: Khush is a software engineer in New York building AI infrastructure and product integrations at Meta.
---
<section class="hero">
  <div class="shell">
    <div class="hero-copy">
      <p class="eyebrow">Last deployed · {{ site.time | date: "%b %-d, %Y" }}</p>
      <h1>Hi, I’m Khush.<br>I build infrastructure for AI products.</h1>
      <div class="hero-deck">
        <p>Software Engineer @ Meta. Pickleball, film, and Thai food enthusiast.</p>
        <p>This site is for me to document my journey tinkering on my personal projects and journaling my learnings. All thoughts are my own.</p>
      </div>
      <nav class="hero-links" aria-label="Introduction links">
        <a href="{{ '/writing/' | relative_url }}">Read my writing <span aria-hidden="true">→</span></a>
        <a href="{{ '/about/' | relative_url }}">About me <span aria-hidden="true">→</span></a>
      </nav>
    </div>
  </div>
</section>

<section class="section section-bordered">
  <div class="shell section-heading">
    <div>
      <p class="eyebrow">Latest notes</p>
      <h2>Writing</h2>
    </div>
    <a class="text-link" href="{{ '/writing/' | relative_url }}">View everything <span aria-hidden="true">→</span></a>
  </div>
  <div class="shell">
    {% include post-list.html posts=site.posts limit=3 %}
  </div>
</section>
