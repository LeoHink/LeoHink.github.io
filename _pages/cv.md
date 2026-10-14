---
layout: page
permalink: /cv/
title: cv
nav: true
nav_order: 5
cv_pdf: CV_LH_online_10_2026.pdf # file in assets/pdf/ — update this when you upload a new CV
description:
_styles: >
  .cv-actions { margin-bottom: 1rem; }
  .cv-actions a.btn { color: var(--global-text-color); border: 1px solid var(--global-text-color); margin: 0 0.5rem 0.5rem 0; }
  .cv-actions a.btn:hover { color: var(--global-theme-color); border-color: var(--global-theme-color); }
  .cv-embed { display: block; width: 100%; height: 85vh; min-height: 500px; border: 1px solid var(--global-divider-color); }
---

{% assign cv_url = page.cv_pdf | prepend: '/assets/pdf/' | relative_url %}

<div class="cv-actions">
  <a href="{{ cv_url }}" class="btn btn-sm z-depth-0" role="button" download><i class="fa-solid fa-download"></i> Download PDF</a>
  <a href="{{ cv_url }}" class="btn btn-sm z-depth-0" role="button" target="_blank" rel="noopener noreferrer"><i class="fa-solid fa-up-right-from-square"></i> Open in new tab</a>
</div>

<object class="cv-embed" data="{{ cv_url }}" type="application/pdf" aria-label="CV of Leonard Hinckeldey">
  <p>Your browser can't display the PDF inline. <a href="{{ cv_url }}">Download the CV</a> instead.</p>
</object>
