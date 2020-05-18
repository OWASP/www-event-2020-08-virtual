---

title: OWASP Virtual AppSec Days April 2020
layout: event

---
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Event",
  "name": "OWASP Virtual AppSec Days April 2020",
  "description": "The OWASP Foundation is hosting a Virtual AppSec Days on April 27-29th. 
        We will be running a 90 minute virtual mini-conference Monday, April 27, 
        followed by 8-hour virtual training courses offered in 4-hour blocks on the 28th-29th. 
        The trainings will begin at 12:00pm Eastern Time (USA)/6:00pm Central European Time.
        The event wraps-up with a hosted by Security Innovation. Put your skills to the test in this 48-hour competition.",
  "startDate": "2020-04-27",
  "endDate": "2020-04-29",
  "eventStatus": "https://schema.org/EventMovedOnline",
  "eventAttendanceMode": "https://schema.org/OnlineEventAttendanceMode",
  "location": {
    "@type": "VirtualLocation",
    "url": "https://appsecdays.org/"
  },
  "offers": [{
    "@type": "Offer",
    "name": "Mini-Conference",
    "price": "0",
    "priceCurrency": "USD",
    "validFrom": "2020-04-07",
    "url": "https://appsecdays.org/",
    "availability": "https://schema.org/InStock"
  },{
    "@type": "Offer",
    "name": "Training Courses",
    "price": "495",
    "priceCurrency": "USD",
    "validFrom": "2020-04-07",
    "url": "https://appsecdays.org/register/",
    "availability": "https://schema.org/InStock"
  },{
    "@type": "Offer",
    "name": "Member Training Courses",
    "price": "445",
    "priceCurrency": "USD",
    "validFrom": "2020-04-07",
    "url": "https://appsecdays.org/register/",
    "availability": "https://schema.org/InStock"
  },{
    "@type": "Offer",
    "name": "CTF",
    "price": "25",
    "priceCurrency": "USD",
    "validFrom": "2020-04-07",
    "url": "https://appsecdays.org/register/",
    "availability": "https://schema.org/InStock"
  }]
}
</script>

<!-- rebuild 10-->

{{ site.data.event-details.pitch | markdownify }}

 **[Check out our sponsors for a chance to win some cool prizes](https://appsecdays.org/sponsors/swag/)**

### Training Sessions hosted 12pm ET (1800 CET) Include


* #### Register for the class you want by clicking below
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

