---
layout: default
title:
description: Khush is a software engineer in New York building AI infrastructure and product integrations at Meta.
---
<section class="hero">
  <div class="shell">
    <section class="now-card now-card-large" aria-labelledby="intro-title">
      <div class="now-card-header">
        <p class="eyebrow">Last deployed · {{ site.time | date: "%b %-d, %Y" }}</p>
        <span class="status-dot" aria-hidden="true"></span>
      </div>
      <h1 id="intro-title" class="now-card-title">Hi! I’m Khush.</h1>
      <dl>
        <div>
          <dt>Career</dt>
          <dd>Product + Infra @ Meta AI</dd>
        </div>
        <div>
          <dt>Hobbies</dt>
          <dd>Pickleball, film &amp; Thai food</dd>
        </div>
        <div>
          <dt>Tinkering</dt>
          <dd>Agentic systems, homelabs &amp; hardware</dd>
        </div>
        <div>
          <dt>Based in</dt>
          <dd>NJ / NYC</dd>
        </div>
      </dl>
      <nav class="now-card-links" aria-label="Introduction links">
        <a href="{{ '/blog/' | relative_url }}">Read the blog <span aria-hidden="true">→</span></a>
        <a href="{{ '/about/' | relative_url }}">More about me <span aria-hidden="true">→</span></a>
      </nav>
      <span class="now-card-mark" aria-hidden="true">KT</span>
    </section>
  </div>
</section>

<section class="section section-bordered">
  <div class="shell section-heading">
    <div>
      <p class="eyebrow">Latest notes</p>
      <h2>Blog</h2>
    </div>
    <a class="text-link" href="{{ '/blog/' | relative_url }}">View all posts <span aria-hidden="true">→</span></a>
  </div>
  <div class="shell">
    {% include post-list.html posts=site.posts limit=3 show_images=true %}
  </div>
</section>
