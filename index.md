---
layout: workshop      # DON'T CHANGE THIS.
carpentry: "swc"    # what kind of Carpentry (must be either "lc" or "dc" or "swc")
venue: "QIMR Berghofer"        # brief name of host site without address (e.g., "Euphoric State University")
address: "Room 311 ITS training, Education Level 3 Central, 300 Herston Rd Herston QLD"      # full street address of workshop (e.g., "Room A, 123 Forth Street, Blimingen, Euphoria")
country: "au"      # lowercase two-letter ISO country code such as "fr" (see https://en.wikipedia.org/wiki/ISO_3166-1)
language: "en"     # lowercase two-letter ISO language code such as "fr" (see https://en.wikipedia.org/wiki/ISO_639-1)
latlng: "-27.449561, 153.027266"       # decimal latitude and longitude of workshop venue (e.g., "41.7901128,-87.6007318" - use https://www.latlong.net/)
humandate: "Sep 25-26, 2018"    # human-readable dates for the workshop (e.g., "Feb 17-18, 2020")
humantime: "9:00 am - 4:30 pm"    # human-readable times for the workshop (e.g., "9:00 am - 4:30 pm")
startdate: 2018-09-25      # machine-readable start date for the workshop in YYYY-MM-DD format like 2015-01-01
enddate: 2018-09-26        # machine-readable end date for the workshop in YYYY-MM-DD format like 2015-01-02
instructor: ["Conrad Leonard", "Scott Wood"] # boxed, comma-separated list of instructors' names as strings, like ["Kay McNulty", "Betty Jennings", "Betty Snyder"]
helper: []     # boxed, comma-separated list of helpers' names, like ["Marlyn Wescoff", "Fran Bilas", "Ruth Lichterman"]
email: ["conrad.leonard@qimrberghofer.edu.au"]    # boxed, comma-separated list of contact email addresses for the host, lead instructor, or whoever else is handling questions, like ["marlyn.wescoff@example.org", "fran.bilas@example.org", "ruth.lichterman@example.org"]
collaborative_notes:             # optional: URL for the workshop collaborative notes, e.g. an Etherpad or Google Docs document
eventbrite:           # optional: alphanumeric key for Eventbrite registration, e.g., "1234567890AB" (if Eventbrite is being used)
---

{% comment %} See instructions in the comments below for how to edit specific sections of this workshop template. {% endcomment %}

{% comment %}
  HEADER

  Edit the values in the block above to be appropriate for your workshop.
  If the value is not 'true', 'false', 'null', or a number, please use
  double quotation marks around the value, unless specified otherwise.
  And run 'make workshop-check' *before* committing to make sure that changes are good.
{% endcomment %}

{% comment %}
  EVENTBRITE

  This block includes the Eventbrite registration widget if
  'eventbrite' has been set in the header.  You can delete it if you
  are not using Eventbrite, or leave it in, since it will not be
  displayed if the 'eventbrite' field in the header is not set.
{% endcomment %}
{% if page.eventbrite %}
<iframe
  src="https://www.eventbrite.com/tickets-external?eid={{page.eventbrite}}&ref=etckt"
  frameborder="0"
  width="100%"
  height="280px"
  scrolling="auto">
</iframe>
{% endif %}

<h2 id="general">General Information</h2>

{% comment %}
  INTRODUCTION

  Edit the general explanatory paragraph below if you want to change
  the pitch.
{% endcomment %}
{% if page.carpentry == "swc" %}
  {% include sc/intro.html %}
{% elsif page.carpentry == "dc" %}
  {% include dc/intro.html %}
{% elsif page.carpentry == "lc" %}
  {% include lc/intro.html %}
{% endif %}

{% comment %}
  AUDIENCE

  Explain who your audience is.  (In particular, tell readers if the
  workshop is only open to people from a particular institution.
{% endcomment %}
{% if page.carpentry == "swc" %}
  {% include sc/who.html %}
{% elsif page.carpentry == "dc" %}
  {% include dc/who.html %}
{% elsif page.carpentry == "lc" %}
  {% include lc/who.html %}
{% endif %}

{% comment %}
  LOCATION

  This block displays the address and links to maps showing directions
  if the latitude and longitude of the workshop have been set.  You
  can use https://itouchmap.com/latlong.html to find the lat/long of an
  address.
{% endcomment %}
{% if page.latlng %}
<p id="where">
  <strong>Where:</strong>
  {{page.address}}.
  Get directions with
  <a href="//www.openstreetmap.org/?mlat={{page.latlng | replace:',','&mlon='}}&zoom=16">OpenStreetMap</a>
  or
  <a href="//maps.google.com/maps?q={{page.latlng}}">Google Maps</a>.
</p>
{% endif %}

{% comment %}
  DATE

  This block displays the date and links to Google Calendar.
{% endcomment %}
{% if page.humandate %}
<p id="when">
  <strong>When:</strong>
  {{page.humandate}}.
  {% include workshop_calendar.html %}
</p>
{% endif %}

{% comment %}
  SPECIAL REQUIREMENTS

  Modify the block below if there are any special requirements.
{% endcomment %}
<p id="requirements">
  <strong>Requirements:</strong>
  <ul>
    <li>Participants must bring a laptop with a
      Mac, Linux, or Windows operating system (not a tablet, Chromebook, etc.)
      They are also required to abide by
      {% if page.carpentry == "swc" %}
      Software Carpentry's
      {% elsif page.carpentry == "dc" %}
      Data Carpentry's
      {% elsif page.carpentry == "lc" %}
      Library Carpentry's
      {% endif %}
    <a href="{{site.swc_site}}/conduct.html">Code of Conduct</a>.
    </li>
    <li>
      An account on the Institute's HPC environment.
    </li>
    <li>
    If using the QIMR-Guest or eduroam wireless networks, users must contact <a href='https://staff.qimr.edu.au/form/itjob'>ITS</a> to ensure they have working access to the QIMR VPN.
    </li> 
    <li>
      An ssh client to connect to the HPC.  On Linux and Mac, this is likely in the base install.  Windows users may need to submit a ticket to <a href='https://staff.qimr.edu.au/form/itjob'>ITS</a> requesting a copy of PuTTY be installed.
    </li>
    <li>
      A X-Server on their laptop.  For Linux laptops, this will likely already be installed.  Windows users may need to submit a ticket to <a href='https://staff.qimr.edu.au/form/itjob'>ITS</a> requesting a copy of XMing be installed.  Mac users may need to submit a ticket to <a href='https://staff.qimr.edu.au/form/itjob'>ITS</a> requesting a copy of XQuartz be installed.
    </li>  
  </ul>
</p>

{% comment %}
  ACCESSIBILITY

  Modify the block below if there are any barriers to accessibility or
  special instructions.
{% endcomment %}
<p id="accessibility">
  <strong>Accessibility:</strong> We are committed to making this workshop
  accessible to everybody.
  The workshop organizers have checked that:
</p>
<ul>
  <li>The room is wheelchair / scooter accessible.</li>
  <li>Accessible restrooms are available.</li>
</ul>
<p>
  Materials will be provided in advance of the workshop and
  large-print handouts are available if needed by notifying the
  organizers in advance.  If we can help making learning easier for
  you (e.g. sign-language interpreters, lactation facilities) please
  get in touch (using contact details below) and we will
  attempt to provide them.
</p>

{% comment %}
  CONTACT EMAIL ADDRESS

  Display the contact email address set in the configuration file.
{% endcomment %}
<p id="contact">
  <strong>Contact</strong>:
  Please email
  {% if page.email %}
    {% for email in page.email %}
      {% if forloop.last and page.email.size > 1 %}
        or
      {% else %}
        {% unless forloop.first %}
        ,
        {% endunless %}
      {% endif %}
      <a href='mailto:{{email}}'>{{email}}</a>
    {% endfor %}
  {% else %}
    to-be-announced
  {% endif %}
  for more information.
</p>

<hr/>

{% comment %} 
 SURVEYS - DO NOT EDIT SURVEY LINKS 
{% endcomment %}
<h2 id="surveys">Surveys</h2>
<p>Please be sure to complete these surveys before and after the workshop.</p>
{% if site.carpentry == "swc" %} 
<p><a href="{{ site.swc_pre_survey }}{{ site.github.project_title }}">Pre-workshop Survey</a></p>
<p><a href="{{ site.swc_post_survey }}{{ site.github.project_title }}">Post-workshop Survey</a></p>
{% elsif site.carpentry == "dc" %}
<p><a href="{{ site.dc_pre_survey }}{{ site.github.project_title }}">Pre-workshop Survey</a></p>
<p><a href="{{ site.dc_post_survey }}{{ site.github.project_title }}">Post-workshop Survey</a></p>
{% elsif site.carpentry == "lc" %}
<p><a href="{{ site.lc_pre_survey }}{{ site.github.project_title }}">Pre-workshop Survey</a></p>
<p><a href="{{ site.lc_post_survey }}{{ site.github.project_title }}">Post-workshop Survey</a></p>
{% endif %}

<hr/>


<h2 id="setup">Setup</h2>
<h3 id="setup-day1">Day 1</h3>
  <p>
  Download the <a href="{{page.root}}/data/shell-novice-data.zip">shell-novice-data.zip</a> file and extract it to your <tt>/working/[lab_head]/[user]</tt> directory on the HPC.
  </p>
<h3 id="setup-day2">Day 2</h3>
  <p>
  Download the <a href="{{page.root}}/data/python-novice-gapminder-data.zip">gapminder dataset</a> and extract it to your <tt>/working/[lab_head]/[user]</tt> directory on the HPC.
  </p>

<hr/>

{% comment %}
  Collaborative Notes

  If you want to use an Etherpad, go to

      http://pad.software-carpentry.org/YYYY-MM-DD-site

  where 'YYYY-MM-DD-site' is the identifier for your workshop,
  e.g., '2015-06-10-esu'.
{% endcomment %}
{% if page.collaborative_notes %}
<h2>Collaborative Notes</h2>
<p id="collaborative_notes">
  We will use this <a href="{{page.collaborative_notes}}">collaborative document</a> for chatting, taking notes, and sharing URLs and bits of code.
</p>
{% endif %}

{% include syllabus.html %}

<hr/>

