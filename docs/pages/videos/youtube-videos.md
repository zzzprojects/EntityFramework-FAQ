---
permalink: youtube-videos
---
<h2>YouTube</h2>
<table>
	<thead>
		<tr>
			<th>Videos</th>
			<th>Description</th>
		</tr>
	</thead>
	<tbody>
{% for video in site.data.videos %}
	{% if video.Kind == "YouTube"%}
		<tr>
			<td>
				<iframe width="560" height="315" src="https://www.youtube.com/embed/{{ video.ID }}" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
			</td>
			<td>
				<h3>{{ video.Title }}</h3>
				{{ video.Description }}
			</td>
		</tr>
	{% endif %}
{% endfor %}		
	</tbody>
</table>
