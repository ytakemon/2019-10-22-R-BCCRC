---
layout: workshop      # DON'T CHANGE THIS.
carpentry: "swc"    # what kind of Carpentry (must be either "lc" or "dc" or "swc").  
                      # Be sure to update the Carpentry type in _config.yml as well.  
venue: "R for Reproducible Reserach"        # brief name of host site without address (e.g., "Euphoric State University")
address: "Diamond Lecture Theatre @ BC Cancer Research Centre, 675 W 10th, Vancouver, Canada"      # full street address of workshop (e.g., "Room A, 123 Forth Street, Blimingen, Euphoria")
country: "ca"      # lowercase two-letter ISO country code such as "fr" (see https://en.wikipedia.org/wiki/ISO_3166-1#Current_codes)
language: "en"     # lowercase two-letter ISO language code such as "fr" (see https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes)
latlng: "49.262580,-123.118720"       # decimal latitude and longitude of workshop venue (e.g., "41.7901128,-87.6007318" - use https://www.latlong.net/)
humandate: "Oct 22-23, 2019"    # human-readable dates for the workshop (e.g., "Feb 17-18, 2020")
humantime: "9:00 am - 4:30 pm"    # human-readable times for the workshop (e.g., "9:00 am - 4:30 pm")
startdate: 2019-10-22     # machine-readable start date for the workshop in YYYY-MM-DD format like 2015-01-01
enddate: 2019-10-23        # machine-readable end date for the workshop in YYYY-MM-DD format like 2015-01-02
instructor: ["Yuka Takemon", "Bruno Grande"] # boxed, comma-separated list of instructors' names as strings, like ["Kay McNulty", "Betty Jennings", "Betty Snyder"]
helper: [""]     # boxed, comma-separated list of helpers' names, like ["Marlyn Wescoff", "Fran Bilas", "Ruth Lichterman"]
email: ["ytakemon@bcgsc.ca"]    # boxed, comma-separated list of contact email addresses for the host, lead instructor, or whoever else is handling questions, like ["marlyn.wescoff@example.org", "fran.bilas@example.org", "ruth.lichterman@example.org"]
collaborative_notes: http://pad.carpentries.org/2019-10-21-BCCRC    # optional: URL for the workshop collaborative notes, e.g. an Etherpad or Google Docs document
eventbrite: "72996609825"           # optional: alphanumeric key for Eventbrite registration, e.g., "1234567890AB" (if Eventbrite is being used)
---
{% comment %}
  Website url: https://ytakemon.github.io/2019-10-22-R-BCCRC
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
This workshop is intended for trainees and staff at BC Cancer with limited or no experience in the R language and/or any form of coding language. We will work towards becoming familiar with how to read and write data, types of data structures, data manipulation, and other forms of general utilities that can help speed up data processing and analyses.

Our goal is to introduce (new) concepts and vocabulary, and most importantly exposure to working in R.

We encourage those with coding experience (python, C, C++, unix, etc.) to help your neighbours!

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

{% if page.humandate %}
<p id="when">
  <strong>When:</strong>
  {{page.humandate}}.
  {% include workshop_calendar.html %}
</p>
{% endif %}

<p id="requirements">
  <strong>Requirements:</strong> Participants must bring a laptop with a
  Mac, Linux, or Windows operating system (not a tablet, Chromebook, etc.) that they have administrative privileges on. They should have a few specific software packages installed (listed <a href="#setup">below</a>).
</p>

<p id="code-of-conduct">
<strong>Code of Conduct:</strong>  Everyone who participates in Carpentries activities is required to conform to the <a href="https://docs.carpentries.org/topic_folders/policies/code-of-conduct.html">Code of Conduct</a>. This document also outlines how to report an incident if needed.
</p>

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

<h2 id="schedule">Schedule</h2>

<div class="row">
<div class="col-md-6">
<h3>Tuesday, October 22nd</h3>
<table class="table table-striped">
<tr> <td>01:00</td>  <td> <a href="https://ytakemon.github.io/2019-10-22-R-BCCRC/">Workshop Overview</a> </td></tr>
<tr> <td>01:10</td>  <td> <a href="https://ytakemon.github.io/2019-10-22-R-BCCRC/01-rstudio-intro/">Introduction to R and RStudio</a> </td></tr>
<tr> <td>01:20</td>  <td> <a href="https://ytakemon.github.io/2019-10-22-R-BCCRC/02-filedir/">Navigating files and directories</a> </td></tr>
<tr> <td>01:40</td>  <td> <a href="https://ytakemon.github.io/2019-10-22-R-BCCRC/02-project-intro/">Project management</a> </td></tr>
<tr> <td>01:50</td>  <td> <a href="https://ytakemon.github.io/2019-10-22-R-BCCRC/03-seeking-help/">Seeking help</a> </td></tr>
<tr> <td>02:00</td>  <td> <a href="https://ytakemon.github.io/2019-10-22-R-BCCRC/15-knitr-markdown/">Producing reports with knitr</a> </td></tr>
<tr> <td>02:30</td>  <td> <a href="https://ytakemon.github.io/2019-10-22-R-BCCRC/04-data-structures-part1/">Understanding data structures</a> </td></tr>
<tr> <td>03:00</td>  <td> <a href="https://ytakemon.github.io/2019-10-22-R-BCCRC/05-data-structures-part2/">Exploring data frames</a> </td></tr>
<tr> <td>03:30</td>  <td> <a href="https://ytakemon.github.io/2019-10-22-R-BCCRC/06-data-subsetting/">Subsetting Data</a> </td></tr>
<tr> <td>03:45</td> <td>Wrap-up</td></tr>
</table>

<h3>Tuesday, October 23rd</h3>
<table class="table table-striped">
<tr> <td>01:00</td>  <td>Recap</td></tr>
<tr> <td>01:15</td>  <td> <a href="https://ytakemon.github.io/2019-10-22-R-BCCRC/07-control-flow/">Control flow</a> </td></tr>
<tr> <td>02:00</td>  <td> <a href="https://ytakemon.github.io/2019-10-22-R-BCCRC/10-functions/">Creating functions</a> </td></tr>
<tr> <td>02:45</td>  <td> <a href="https://ytakemon.github.io/2019-10-22-R-BCCRC/08-plot-ggplot2/">Publication quality graphics</a> </td></tr>
<tr> <td>03:30</td>  <td> <a href="https://ytakemon.github.io/2019-10-22-R-BCCRC/11-writing-data/">Writing data</a> </td></tr>
<tr> <td>03:45</td>  <td>Wrap-up</td></tr>
</table>
</div>
</div>

{% if page.carpentry == "swc" %}
{% include sc/schedule.html %}
{% elsif page.carpentry == "dc" %}
{% include dc/schedule.html %}
{% elsif page.carpentry == "lc" %}
{% include lc/schedule.html %}
{% endif %}

{% if page.collaborative_notes %}
<p id="collaborative_notes">
  We will use this <a href="{{page.collaborative_notes}}">collaborative document</a> for chatting, taking notes, and sharing URLs and bits of code.
</p>
{% endif %}

<hr/>

<h2 id="syllabus">Syllabus</h2>

{% if page.carpentry == "swc" %}
{% include sc/syllabus.html %}
{% elsif page.carpentry == "dc" %}
{% include dc/syllabus.html %}
{% elsif page.carpentry == "lc" %}
{% include lc/syllabus.html %}
{% endif %}

<hr/>

<h2 id="setup">Setup</h2>

<p>
  To participate in a
  {% if page.carpentry == "swc" %}
  Software Carpentry
  {% elsif page.carpentry == "dc" %}
  Data Carpentry
  {% elsif page.carpentry == "lc" %}
  Library Carpentry
  {% endif %}
  workshop,
  you will need access to the software described below.
  In addition, you will need an up-to-date web browser.
</p>
<p>
  We maintain a list of common issues that occur during installation as a reference for instructors
  that may be useful on the
  <a href = "{{site.swc_github}}/workshop-template/wiki/Configuration-Problems-and-Solutions">Configuration Problems and Solutions wiki page</a>.
</p>

<div id="r"> {% comment %} Start of 'R' section. {% endcomment %}
  <h3>R</h3>

  <p>
    <a href="https://www.r-project.org">R</a> is a programming language
    that is especially powerful for data exploration, visualization, and
    statistical analysis. To interact with R, we use
    <a href="https://www.rstudio.com/">RStudio</a>.
  </p>

  <div>
    <ul class="nav nav-tabs nav-justified" role="tablist">
      <li role="presentation" class="active"><a data-os="windows" href="#rstats-windows" aria-controls="Windows" role="tab" data-toggle="tab">Windows</a></li>
      <li role="presentation"><a data-os="macos" href="#rstats-macos" aria-controls="MacOS" role="tab" data-toggle="tab">MacOS</a></li>
      <li role="presentation"><a data-os="linux" href="#rstats-linux" aria-controls="Linux" role="tab" data-toggle="tab">Linux</a></li>
    </ul>

    <div class="tab-content">
      <article role="tabpanel" class="tab-pane active" id="rstats-windows">
        <a href="https://www.youtube.com/watch?v=q0PjTAylwoU">Video Tutorial</a>
        <p>
          Install R by downloading and running
          <a href="https://cran.r-project.org/bin/windows/base/release.htm">this .exe file</a>
          from <a href="https://cran.r-project.org/index.html">CRAN</a>.
          Also, please install the
          <a href="https://www.rstudio.com/products/rstudio/download/#download">RStudio IDE</a>.
          Note that if you have separate user and admin accounts, you should run the
          installers as administrator (right-click on .exe file and select "Run as
          administrator" instead of double-clicking). Otherwise problems may occur later,
          for example when installing R packages.
        </p>
      </article>
      <article role="tabpanel" class="tab-pane active" id="rstats-macos">
        <a href="https://www.youtube.com/watch?v=5-ly3kyxwEg">Video Tutorial</a>
        <p>
          Install R by downloading and running
          <a href="https://cran.r-project.org/bin/macosx/R-latest.pkg">this .pkg file</a>
          from <a href="https://cran.r-project.org/index.html">CRAN</a>.
          Also, please install the
          <a href="https://www.rstudio.com/products/rstudio/download/#download">RStudio IDE</a>.
        </p>
      </article>
      <article role="tabpanel" class="tab-pane active" id="rstats-linux">
        <p>
          You can download the binary files for your distribution
          from <a href="https://cran.r-project.org/index.html">CRAN</a>. Or
          you can use your package manager (e.g. for Debian/Ubuntu
          run <code>sudo apt-get install r-base</code> and for Fedora run
          <code>sudo dnf install R</code>).  Also, please install the
          <a href="https://www.rstudio.com/products/rstudio/download/#download">RStudio IDE</a>.
        </p>
      </article>
    </div>
  </div>
</div> {% comment %} End of 'R' section. {% endcomment %}
