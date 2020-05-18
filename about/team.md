---

title: The Conference Team
layout: event_noheader
registration_url: /register/
permalink: about/team/

---

# {{ page.title }}
<br>
<section class="team-list">
	<h3>Organizing Committee</h3>
	<ul >
	{% for member in site.data.team.conferenceteam %}
	<li>
		<div style="background-image: url(/assets/images/team/{{member.image | default: 'owasp_logo.png'}})" alt="{{member.name}} {{member.role}}"></div>
		<h4>{{member.name}}</h4>
		<span class="role">{{member.role}}</span>
	</li>
	{% endfor %}
	</ul>
</section>
<section class="team-list">
	<h3>OWASP Staff</h3>
	<ul>
	{% for member in site.data.team.staff %}
	<li>
		<div style="background-image: url(/assets/images/team/{{member.image | default: 'owasp_logo.png'}})" alt="{{member.name}} {{member.role}}"></div>
		<h4>{{member.name}}</h4>
		<span class="role">{{member.role}}</span>
	</li>
	{% endfor %}
	</ul>
</section>

