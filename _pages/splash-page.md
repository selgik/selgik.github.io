---
title: "Sylvia's Learning Log"
layout: splash
permalink: /splash-page/
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  overlay_image: /assets/splash/da.jpg

actions:
    - label: "Read Posts"
      url: "https://selgik.github.io/"
      
intro: 
  - excerpt: 'Check out my latest data analytic projects here!'
  
feature_row:
  - image_path: /assets/splash/pic1_e.png
    title: "Placeholder 1"
    excerpt: "Sample text 1 with **markdown** formatting."
    url: "#test-link"
    btn_label: "Read More"
    btn_class: "btn--primary"
  - image_path: /assets/splash/pic2_t.png
    title: "Placeholder 2"
    excerpt: "This is some sample content that goes here with **Markdown** formatting."
    url: "#test-link"
    btn_label: "Read More"
    btn_class: "btn--secondar"
  - image_path: /assets/splash/pic3_r.png
    title: "Placeholder 3"
    excerpt: "This is some sample content that goes here with **Markdown** formatting."
    url: "#test-link"
    btn_label: "Read More"
    btn_class: "btn--primary"
---
<!--- Below is needed to add intro --->
{% include feature_row id="intro" type="center" %}

<!--- Below is needed to add row division --->
{% include feature_row %}
