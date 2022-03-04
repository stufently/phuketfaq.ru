---
layout: faq
---
{% assign faqsize = site.data.faq | map: 'items' | flatten | where:"ldjson", true | size %}

{%- if site.data.faq -%}
{%- if faqsize -%}
{%- assign schema_items = site.data.faq | map: 'items' | flatten | where:"ldjson", true | faq_items | join: "," -%}
<script type="application/ld+json">{"@context":"https://schema.org","@type":"FAQPage","mainEntity": {{ schema_items }} }</script>
{%- endif -%}
{%- endif -%}

{% for group in site.data.faq %}

- [{{ group.question }}](#{{ group.hashtag }})
  {% for item in group.items %}- [{{ item.question }}](#{{ item.hashtag }})
  {% endfor %} {% endfor %}

{% for group in site.data.faq %}

# <a name="{{ group.hashtag }}"></a>{{ group.question }}

{% for item in group.items %}

## <a name="{{ item.hashtag }}"></a>{{ item.question }}

{{ item.answer }} {% endfor %} {% endfor %}