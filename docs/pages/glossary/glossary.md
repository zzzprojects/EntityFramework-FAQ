---
permalink: glossary
---

{% assign glossary_category = "default" %}

{% for item in site.data.glossary %}

{% if item.category != glossary_category %}

{% if item != site.data.glossary[0] %}
</table>
{% endif %}
{% assign glossary_category = item.category %}
<h2 id="{{ item.category }}">{{ item.category }}</h2>
<table>
<thead>
	<tr>
		<th>Term</th>
		<th>Definition</th>
	</tr>
</thead>
{% endif %}
<tr>
	<td>{{ item.term }}</td>
	<td>{{ item.definition }}</td>
</tr>

{% endfor %}
</table>