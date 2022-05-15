---
title: "Sylvia's Learning Log"
layout: splash
permalink: /splash-page/
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  overlay_image: /assets/splash/da.jpg

  actions:
    - label: "Learn More"
      url: "https://selgik.github.io/"
      
intro: 
  - excerpt: 'Welcome to my blog! My name is Sylvia and I am curious about numbers, data and stories behind them. Check out my latest data analytic portfolio below!'
  
feature_row:
  - image_path: /assets/splash/pic1_e.png
    title: "Excel VBA Project"
    excerpt: "Sample text 1 with **markdown** formatting."
    url: "#test-link"
    btn_label: "Read More"
    btn_class: "btn--inverse"
  - image_path: /assets/splash/pic2_t.png
    title: "Tableau Dashboards"
    excerpt: "This is some sample content that goes here with **Markdown** formatting."
    url: "#test-link"
    btn_label: "Read More"
    btn_class: "btn--inverse"
  - image_path: /assets/splash/pic3_r.png
    title: "R Markdown Review"
    excerpt: "This is some sample content that goes here with **Markdown** formatting."
    url: "#test-link"
    btn_label: "Read More"
    btn_class: "btn--inverse"
---
<!--- Below is needed to add intro --->
{% include feature_row id="intro" type="center" %}

<!--- Below is needed to add row division --->
{% include feature_row %}
