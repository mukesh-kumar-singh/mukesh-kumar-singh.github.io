---
permalink: /publications/
title: "Publications"
layout: single
author_profile: true
---

<style>
.pub-list { counter-reset: pub-counter; margin-top: 1em; }
.pub-year-heading {
  font-size: 1.1em;
  font-weight: 700;
  letter-spacing: 0.04em;
  text-transform: uppercase;
  opacity: 0.6;
  margin: 1.6em 0 0.6em;
  border-bottom: 1px solid rgba(128,128,128,0.3);
  padding-bottom: 0.2em;
}
.pub-year-heading:first-child { margin-top: 0; }
.pub-card {
  counter-increment: pub-counter;
  position: relative;
  padding: 0.9em 1em 0.9em 2.6em;
  margin-bottom: 0.7em;
  border-radius: 10px;
  background: rgba(128, 128, 128, 0.08);
  border: 1px solid rgba(128, 128, 128, 0.18);
  transition: background 0.15s ease, transform 0.15s ease;
}
.pub-card:hover {
  background: rgba(128, 128, 128, 0.15);
  transform: translateX(2px);
}
.pub-card::before {
  content: counter(pub-counter);
  position: absolute;
  left: 0.8em;
  top: 0.95em;
  font-weight: 700;
  font-size: 0.85em;
  opacity: 0.5;
}
.pub-title {
  font-weight: 600;
  font-size: 1.02em;
  margin: 0 0 0.25em;
}
.pub-authors { font-size: 0.95em; margin-bottom: 0.4em; opacity: 0.9; }
.pub-authors .me { font-weight: 700; }
.pub-meta { font-size: 0.88em; opacity: 0.75; margin-bottom: 0.5em; }
.pub-links { display: flex; flex-wrap: wrap; gap: 0.5em; }
.pub-badge {
  display: inline-block;
  font-size: 0.78em;
  font-weight: 600;
  padding: 0.15em 0.65em;
  border-radius: 999px;
  text-decoration: none !important;
  border: 1px solid currentColor;
  opacity: 0.85;
}
.pub-badge:hover { opacity: 1; }
.pub-badge.arxiv { color: #b31b1b; }
.pub-badge.journal { color: #2b6cb0; }
.pub-badge.status { color: #6b7280; border-style: dashed; }
</style>

<div class="pub-list">
{% assign pubs_by_year = site.data.publications | group_by: "year" | sort: "name" | reverse %}
{% for group in pubs_by_year %}
  <div class="pub-year-heading">{{ group.name }}</div>
  {% for pub in group.items %}
  <div class="pub-card">
    <p class="pub-title">{{ pub.title }}</p>
    <p class="pub-authors">
      {% for a in pub.authors %}{% if a.highlight %}<span class="me">{{ a.name }}</span>{% else %}{{ a.name }}{% endif %}{% unless forloop.last %}, {% endunless %}{% endfor %}
    </p>
    {% if pub.venue %}<p class="pub-meta">{{ pub.venue }}</p>{% endif %}
    <div class="pub-links">
      {% if pub.links.arxiv %}<a class="pub-badge arxiv" href="{{ pub.links.arxiv }}" target="_blank" rel="noopener">arXiv</a>{% endif %}
      {% if pub.links.journal %}<a class="pub-badge journal" href="{{ pub.links.journal }}" target="_blank" rel="noopener">Journal</a>{% endif %}
      {% if pub.status %}<span class="pub-badge status">{{ pub.status }}</span>{% endif %}
    </div>
  </div>
  {% endfor %}
{% endfor %}
</div>
