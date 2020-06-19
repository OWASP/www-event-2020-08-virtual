---

title: Schedule & Trainings
layout: event_noheader
permalink: /

---

<link rel="stylesheet" type="text/css" href="/assets/css/training.css">

# {{ page.title }}
<br>

**Tuesday, August 25** and **Wednesday, August 26** 
* Virtual Training Courses
* 12:00pm to 4:00pm EDT/1800pm to 2200pm CET 

### **Please note: All courses take place simultaneously over two days, only register for one.**

**Training subject to change based on trainer availability.**
{% if site.data.trainings.size > 0 %}
{% assign trainings = site.data.trainings | sort: 'Title' %}
{% for trainer in trainings %}
<section class="trainer-section" id="{{trainer.SectionId}}">
<hr>
<ul>
<li><h3 class='training-header'>{{ trainer.Title }}<button class="cta-button grey" {%if trainer.Status == 'Postponed' or trainer.Status == 'Canceled' %}disabled='true' {%endif%} onclick="location.href='{{trainer.URL}}';" style="margin-left:1em;cursor: pointer;max-width=80px;">{%if trainer.Status == 'Postponed' or traner.Status == 'Canceled'%}{{trainer.Status}}{%else%}Register{%endif%}</button></h3></li>
<li class="training-desc">{{ trainer.Description }}</li>
    <ul>
        {% for tr in trainer.Trainers %}
        <li><div class="training-container"><a href="/trainers/#{{tr.TrainerId}}" title="{{tr.Biography | strip_html}}"><div class="training-image" style="background-image:url('{{tr.Image}}');"></div>{{tr.Name}}</a></div></li>
        {% endfor %}
    </ul>
</ul>
</section>
{% endfor %}
{% endif %}
