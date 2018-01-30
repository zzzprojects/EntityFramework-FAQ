---
permalink: general-blog
---

<h2>General's Blog</h2>

<table>
	<tbody>
{% for blog in site.data.blogs %}
	{% if blog.Kind == "General" %}
		<tr>
			<td>
				<h3><a href="{{ blog.Url }}">{{ blog.Title }}</a></h3>
				{{ blog.Description }}
			</td>
		</tr>
	{% endif %}
{% endfor %}
				
	</tbody>
</table>

