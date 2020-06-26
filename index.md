---

title: AppSec Days - August 2020
layout: event

---
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Event",
  "name": "AppSec Days - Summer of Security 2020",
  "description": "The OWASP Foundation is hosting virtual AppSec Days on the last Tuesday and Wednesday in June, July, and August. 
        The trainings will begin at 12:00pm Eastern Time (USA)/6:00pm Central European Time.",
  "startDate": "2020-06-23",
  "endDate": "2020-08-26",
  "eventStatus": "https://schema.org/EventMovedOnline",
  "eventAttendanceMode": "https://schema.org/OnlineEventAttendanceMode",
  "location": {
    "@type": "VirtualLocation",
    "url": "https://appsecdays.org/"
  },
  "offers": [{
    "@type": "Offer",
    "name": "Training Courses",
    "price": "495",
    "priceCurrency": "USD",
    "validFrom": "2020-05-20",
    "url": "https://appsecdays.org/register/",
    "availability": "https://schema.org/InStock"
  },{
    "@type": "Offer",
    "name": "Member Training Courses",
    "price": "445",
    "priceCurrency": "USD",
    "validFrom": "2020-05-20",
    "url": "https://appsecdays.org/register/",
    "availability": "https://schema.org/InStock"
  }]
}
</script>

<!-- rebuild 11-->

{{ site.data.event-details.pitch | markdownify }}

 **[Check out our sponsors for a chance to win some cool prizes](https://appsecdays.org/sponsors/swag/)**

### Training Sessions hosted 12pm ET (1800 CET) Include


* #### Join us for the class you want by clicking below
* Please note: All courses take place simultaneously over 2 days, only register for 1.
* *(more information can be found on the [Training](/trainings/) page)*
{% if site.data.trainings.count > 0 %}
<ul>
  {% assign trainings = site.data.trainings | sort: 'Title' %}
  {% for trainer in trainings %}
    <li><a href="{{trainer.URL}}">{{ trainer.Title }}</a></li>
  {% endfor %}
</ul>
{% endif %}

