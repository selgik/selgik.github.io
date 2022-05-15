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
  - excerpt: 'I am curious about numbers, data and stories behind them! And I love solving problems with Macro, SQL, Tableau and R! Check out my latest portfolio below!'
  
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
