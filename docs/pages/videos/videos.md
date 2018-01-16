---
permalink: videos
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
	{% if video.Kind == "YouTube" and video.Pinned == "1" %}
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

<a href="{{ site.github.url }}/youtube-videos">more videos...</a>

<h2>Lynda</h2>
<table>
	<thead>
		<tr>
			<th>Videos</th>
			<th>Description</th>
		</tr>
	</thead>
	<tbody>
{% for video in site.data.videos %}
	{% if video.Kind == "Lynda"  and video.Pinned == "1" %}
		<tr>
			<td>
				<iframe width='560' height='315' src='https://www.lynda.com/player/embed/{{ video.ID }}?fs=3&w=560&h=315&ps=paused&utm_medium=referral&utm_source=embed+video&utm_campaign=ldc-website&utm_content=vid-{{ video.ID }}' mozallowfullscreen='true' webkitallowfullscreen='true' allowfullscreen='true' frameborder='0'></iframe>
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

<a href="{{ site.github.url }}/lynda-videos">more videos...</a>

<h3>Channel 9</h3>
<table>
	<thead>
		<tr>
			<th>Videos</th>
			<th>Description</th>
		</tr>
	</thead>
	<tbody>
{% for video in site.data.videos %}
	{% if video.Kind == "Channel9" and video.Pinned == "1" %}
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

<a href="{{ site.github.url }}/channel9-videos">more videos...</a>

<h3>Pluralsight</h3>
<ul>
	<li><a href="https://app.pluralsight.com/library/courses/entity-framework-6-getting-started/table-of-contents">Getting Started with Entity Framework 6</a></li>
    <li><a href="https://app.pluralsight.com/library/courses/entity-framework-core-getting-started/table-of-contents">Entity Framework Core: Getting Started</a></li>
    <li><a href="https://app.pluralsight.com/library/courses/play-by-play-ef-core-1-0-first-look-julie-lerman/table-of-contents">EF Core 1.0: First Look</a></li>
    <li><a href="https://app.pluralsight.com/library/courses/code-first-entity-framework-legacy-databases/table-of-contents">Code-first Entity Framework with Legacy Databases</a></li>
    <li><a href="https://app.pluralsight.com/library/courses/entity-framework-enterprise-update/table-of-contents">Entity Framework in the Enterprise</a></li>
    <li><a href="https://app.pluralsight.com/library/courses/entity-framework-7-looking-ahead/table-of-contents">Looking Ahead to Entity Framework 7</a></li>
    <li><a href="https://app.pluralsight.com/library/courses/efmigrations/table-of-contents">Entity Framework Code First Migrations</a></li>
    <li><a href="https://app.pluralsight.com/library/courses/efintro-models/table-of-contents">Entity Framework and Data Models</a></li>
    <li><a href="https://app.pluralsight.com/library/courses/querying-entity-framework/table-of-contents">Querying the Entity Framework</a></li>
</ul>
<h3>Udemy</h3>	
<ul>
	<li><a href="https://www.udemy.com/entity-framework-a-comprehensive-course/">Entity Framework : A Comprehensive Course</a></li>
    <li><a href="https://www.udemy.com/entity-framework-tutorial/">Entity Framework in Depth: The Complete Guide</a></li>
    <li><a href="https://www.udemy.com/learn-entity-framework-core-2-efc2-using-aspnet-core/">Learn Entity Framework Core 2.0 (EFC2) using ASP.Net Core</a></li>
    <li><a href="https://www.udemy.com/aspnet-mvc-with-entity-framework-from-scratch/">Asp.Net MVC With Entity Framework From Scratch</a></li>
    <li><a href="https://www.udemy.com/mastering-entity-framework-core-mapping-manipulating-data/">Mastering Entity Framework Core: Mapping & Manipulating Data</a></li>
    <li><a href="https://www.udemy.com/learn_aspnet_bootstrap_entityframework/">Learn ASP NET with Bootstrap,Entity Framework,JavaScript,C#</a></li>
    <li><a href="https://www.udemy.com/learn-aspnet-core-mvc-web-apis-ef-core-bonus-ios-app/">Learn ASP.NET Core using MVC 6 and Entity Framework Core 1.0</a></li>
    <li><a href="https://www.udemy.com/learning-path-mastering-entity-framework-core/">Learning Path: Mastering Entity Framework Core</a></li>
    <li><a href="https://www.udemy.com/learning-entity-framework-core/">Learning Entity Framework Core</a></li>
    <li><a href="https://www.udemy.com/mastering-entity-framework-core-migrations-testing/">Mastering Entity Framework Core - Migrations & Testing</a></li>
</ul>
<h3>Microsoft Virtual Academy</h3>
<ul>
    <li><a href="https://mva.microsoft.com/en-US/training-courses/implementing-entity-framework-with-mvc-8931?l=e2H2lDC3_8304984382">Implementing Entity Framework with MVC</a></li>
</ul>

<h3>Others</h3>
<ul>
	<li><a href="https://codewithmosh.teachable.com/p/entity-framework/?coupon_code=HALFOFF">Entity Framework 6 in Depth</a></li>
	<li><a href="https://www.wintellectnow.com/Videos/Watch?videoId=code-first-development-with-entity-framework">Code-First Development with Entity Framework</a></li>
</ul>