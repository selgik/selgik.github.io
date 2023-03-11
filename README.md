# Change Log
I am using this page to track changes, leave notes and reference pages. To review original README.md, please go to this [link](https://github.com/mmistakes/minimal-mistakes)

## 2023-03-12
- created _posts/2023-03-11-Python-GUI.md and linked URL on splash page. Removed (1) changed date on _posts/2022-06-01-R-code-note.md (2) and removed from splash page

## 2022-05-16
- created 2022-05-01-VBA-project.md and linked URL on splash page. Removed (1) 2022-02-04-project-note.md (2) 2022-02-05-vba-note.md
- created 2022-05-03-Tableau-dashboards.md and linked URL on splash page. Removed (1) 2022-02-03-tableau-code-note.md (2) 2022-02-02-sql-note.md
- created 2022-02-01-data-viz.md(old). Original 2022-02-01-data-viz.md --> rediretred to splash page.

## 2022-05-15
- created splash page (ref [Jan's blog](https://www.janmeppe.com/blog/how-to-add-splash-to-minimal-mistakes/), [Raw Gist](https://gist.githubusercontent.com/Rainymood/35ae7d900f4d8a3d3199ee20fefe2567/raw/6722ecc4e160196b9d1aae01d91ca4d51e522e46/splash-page.md))
- nulled original splash-page.md by changing its name as splash-page.md2
- created new one with its name as splash-page.md

- changed minimal_mistakes_skin from air to contrast on config.yml
- removed title name on config.yml
- changed url on _data/navigation.yml 
- added "Posts" section on _data/navigation.yml 

## 2022-02-07
- changed date format under /_posts to re-arrange the order of posts.
- added one more navigation (tableau demo) under _data/navigation.yml

#### Reference
- [jekyll blog basic-kokr](https://dreamgonfly.github.io/blog/jekyll-remote-theme/)

## 2022-02-06
- created posts/template, posts/2022-02-06/..
- created /_includes/video1.html
- added video1.mp4 to asset/images/
- added plugin(gem) in_config/yml (line 231: - jekyll-redirect-from)
- changed navigation setting: /_data/navigation.yml

#### How to add video to post
1. upload video to /asset/images
2. create html file in /_includes/"filename".html see iframe code (ref: /asset/images/video1.html)
3.  add body in /_posts/"post".md 

        {% include video1.html id="/assets/images/video1.mp4" %}  
#### How to redirect post page -> external url
1. [Review JekyllRedirectFrom](https://github.com/jekyll/jekyll-redirect-from)
2. add plug-in
3. add YAML in the post

       title: "abcd"
       redirect_to: https://..

#### Reference:
- [jekyll doc](https://jekyllrb.com/docs/posts/)
- [toc ref link](https://github.com/devinlife/devinlife.github.io/commit/c48ecb7cab54575bba802a3703dc5dc65d23c92c?diff=split)
- [toc ref link2](https://devinlife.com/howto%20github%20pages/toc-table/)
- [how to insert mp4: seanlion blog1](https://seanlion.github.io/blog/4) 
- [how to insert mp4: TToJ blog2](https://ttoj.github.io/diary/github/How_to_insert_mp4_on_GitHub_blog/)
- RMD to MD compliling reference: [eroubenoff blog](http://www.eroubenoff.net/2021-03-10-rmarkdown_jekyll/)
