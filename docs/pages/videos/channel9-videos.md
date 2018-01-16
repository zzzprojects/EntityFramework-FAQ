---
permalink: channel9-videos
---
<h2>Channel 9</h2>
<table>
	<thead>
		<tr>
			<th>Videos</th>
			<th>Description</th>
		</tr>
	</thead>
	<tbody>
{% for video in site.data.videos %}
	{% if video.Kind == "Channel9" %}
		<tr>
			<td>
                <iframe width='560' height='315' src="https://channel9.msdn.com/{{ video.ID }}/player?format=smooth" mozallowfullscreen='true' webkitallowfullscreen='true' allowFullScreen frameBorder="0"></iframe>
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
