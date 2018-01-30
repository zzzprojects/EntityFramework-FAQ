---
permalink: blogs
---

<h2>Devmate's Blog</h2>

<table>
	<tbody>
{% for blog in site.data.blogs %}
	{% if blog.Kind == "Devmate" and blog.Pinned == "1" %}
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

<a href="{{ site.github.url }}/devmate-blog">See more Devmate's posts...</a>

<h2>Dixin's Blog</h2>

<table>
	<tbody>
{% for blog in site.data.blogs %}
	{% if blog.Kind == "Dixin" and blog.Pinned == "1" %}
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

<a href="{{ site.github.url }}/dixin-blog">See more Dixin's posts...</a>

<h2>.Net Blog</h2>

<table>
	<tbody>
{% for blog in site.data.blogs %}
	{% if blog.Kind == ".Net" and blog.Pinned == "1" %}
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

<a href="{{ site.github.url }}/dot-net-blog">See more posts...</a>

<h2>Tony Sneed's Blog</h2>

<table>
	<tbody>
{% for blog in site.data.blogs %}
	{% if blog.Kind == "TonySneed" and blog.Pinned == "1" %}
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

<a href="{{ site.github.url }}/tony-sneed-blog">See more TonySneed's posts...</a>

<h2>JetBrains Blog</h2>

<table>
	<tbody>
{% for blog in site.data.blogs %}
	{% if blog.Kind == "JetBrains" and blog.Pinned == "1" %}
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

<a href="{{ site.github.url }}/jet-brains-blog">See more JetBrains's posts...</a>

<h2>Telerik's Blog</h2>

<table>
	<tbody>
{% for blog in site.data.blogs %}
	{% if blog.Kind == "Telerik" and blog.Pinned == "1" %}
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

<a href="{{ site.github.url }}/telerik-blog">See more Telerik's posts...</a>

<h2>CSharpCorner's Blog</h2>

<table>
	<tbody>
{% for blog in site.data.blogs %}
	{% if blog.Kind == "CSharpCorner" and blog.Pinned == "1" %}
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

<a href="{{ site.github.url }}/csharp-corner-blog">See more CSharpCorner's posts...</a>

<h2>OneUnicorn's Blog</h2>

<table>
	<tbody>
{% for blog in site.data.blogs %}
	{% if blog.Kind == "OneUnicorn" and blog.Pinned == "1" %}
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

<a href="{{ site.github.url }}/one-unicorn-blog">See more OneUnicorn's posts...</a>