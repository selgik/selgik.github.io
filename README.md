Changelog

### 2022-02-06
- created posts/template, posts/2022-02-06/..
- created /_includes/video1.html  
- added video1.mp4 to asset/images/
- added plugin(gem) in_config/yml (line 231: - jekyll-redirect-from)

#### How to add video to post
- upload video to /asset/images
- create html file in /_includes/"filename".html see iframe code (ref: /asset/images/video1.html)
- add body in /_posts/"post".md 

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
