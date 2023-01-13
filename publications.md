---
layout: single
title: Publications
permalink: /publications/
---

## Journal Papers

{% for item in site.data.publications.journals %}

\[{{ forloop.length | minus: forloop.index0 }}\]
<!-- Author, bold D. P. Nguyen -->
{% for author in item.authors %}
  {%- if author == "D. P. Nguyen" -%}
  **{{ author }}**,&nbsp;
  {%- else -%}
  {{ author }},&nbsp;
  {%- endif -%}
{% endfor %}
<!-- Title and journal name -->
"{{ item.title }}," *{{ item.journal }}*
{%- if item.vol -%}
, vol. {{ item.vol }}
{%- endif -%}
{%- if item.page -%}
, pp. {{ item.page }}
{%- endif -%}
, {{ item.date }}
<!-- Links -->
{%- if item.pdf -%}
[[PDF]]({{ item.pdf }}) 
{%- endif -%}
{%- if item.code -%}
[[Code]]({{ item.code }})
{%- endif -%}
{%- if item.blog -%}
[[Blog]]({{ item.blog }})
{%- endif -%}

{% endfor %}
<br>


## Conference Papers

{% for item in site.data.publications.conferences %}

\[{{ forloop.length | minus: forloop.index0 }}\]
<!-- Author, bold D. P. Nguyen -->
{% for author in item.authors %}
  {%- if author == "D. P. Nguyen" -%}
  **{{ author }}**,&nbsp;
  {%- else -%}
  {{ author }},&nbsp;
  {%- endif -%}
{% endfor %}
<!-- Title, journal name and year -->
"{{ item.title }}," *{{ item.conf }}*, {{ item.year }}
{%- if item.page -%}
, pp. {{ item.page }}
{%- endif -%}
<!-- Links -->
{%- if item.pdf -%}
&nbsp;[[PDF]]({{ item.pdf }}) 
{%- endif -%}
{%- if item.code -%}
[[Code]]({{ item.code }})
{%- endif -%}

{% endfor %}
<br>


## Preprints

{% for item in site.data.publications.preprints %}

\[{{ forloop.length | minus: forloop.index0 }}\]
<!-- Author, bold D. P. Nguyen -->
{% for author in item.authors %}
  {%- if author == "D. P. Nguyen" -%}
  **{{ author }}**,&nbsp;
  {%- else -%}
  {{ author }},&nbsp;
  {%- endif -%}
{% endfor %}
<!-- Title, journal name and date -->
"{{ item.title }}," *{{ item.journal }}*, {{ item.date }}
<!-- Links -->
[[PDF]]({{ item.pdf }}) 
{%- if item.code -%}
[[Code]]({{ item.code }})
{%- endif -%}

{% endfor %}
<br>


## Other

{% for item in site.data.publications.other %}

\[{{ forloop.length | minus: forloop.index0 }}\]
<!-- Author, bold D. P. Nguyen -->
{% for author in item.authors %}
  {%- if author == "D. P. Nguyen" -%}
  **{{ author }}**,&nbsp;
  {%- else -%}
  {{ author }},&nbsp;
  {%- endif -%}
{% endfor %}
<!-- Title and journal name -->
"{{ item.title }}," *{{ item.publisher }}*, {{ item.date }}
<!-- Links -->
{%- if item.pdf -%}
[[PDF]]({{ item.pdf }}) 
{%- endif -%}
{%- if item.code -%}
[[Code]]({{ item.code }})
{%- endif -%}

{% endfor %}