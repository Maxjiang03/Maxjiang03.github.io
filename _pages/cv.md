---
layout: archive
title: "CV"
permalink: /cv/
author_profile: true
---

{% include base_path %}

{% assign cv_pdf = site.static_files | where: "path", "/files/Yixian_Jiang_CV.pdf" | first %}
{% if cv_pdf %}
You can download my CV here: [**Yixian Jiang — CV (PDF)**](/files/Yixian_Jiang_CV.pdf).
{% else %}
*A public, redacted version of my CV will be available here shortly.*
{% endif %}

<!--
IMPORTANT (privacy): place a PUBLIC, REDACTED version of your CV at files/Yixian_Jiang_CV.pdf.
Before publishing, REMOVE your phone number, home address, and matric/student number —
your current source CV contains all three. Once that file is added, the download link
above appears automatically (no further edits needed).
-->
