[TOC levels=1-3]: #

# Table of Contents
- [What can I find in this Blog ?](#what-can-i-find-in-this-blog-)
- [Does this website respect my privacy ?](#does-this-website-respect-my-privacy-)
- [How to give feedback on an article ?](#how-to-give-feedback-on-an-article-)
- [What tech stack has been used to build this blog ?](#what-tech-stack-has-been-used-to-build-this-blog-)



# What can I find in this Blog ?
[*https://oussamahaff.dev*](https://oussamahaff.dev) is my personal blog
where I'll be sharing my knowledge about :
- Mobile Apps engineering especially `Android`
- Software `Craftsmanship`
- My `own views` on tech in general
- All articles, except views, are `reviewed` by `trusted` engineer(s) in the community
- All articles have a `transparent` modification history

# Does this website respect my privacy ?
This blog simply :
- has `no ads`
- has `no trackers`
- has `no SEO scripts`
- does `not use cookies`
- does `not collect` / does `not store` / does `not share` any user data

It's a static site, generated from markdown files. You can read about
how it's made further in this article.

<img src="static/img/00_the_blog_s_readme/no_trackers_no_cookies.webp"
alt="Captured from Brave browser on strict privacy mode. No privacy
tradeoffs !" style="float: center; border-radius: 8px;" />


# How to give feedback on an article ?
Comments plugins hides generally cross-site tracker. As an alternative,
you will find in every article a link to
[***create a Github issue***](https://github.com/hfrsoussama/oussamahaff_dev/issues/new/choose)
on the blog's *Github* repository. Templates for different types of
comments and feedbacks are **already filled** for you with basic
information.

You will be able to :
- ask a question
- suggest an improvement for an article or for the whole website
- alert the author about a deprecated content
- give a general feedback

<img
src="static/img/00_the_blog_s_readme/github_issues_for_comments.webp"
alt="To avoid comments plugin that track you, I've made *Github*
templates ready for you :)"
style="float: center; border-radius: 8px;" />

# What tech stack has been used to build this blog ?
For optimal speed and security, the blog is built using what's called the
[*JAM Stack*](https://jamstack.org)
- Pages and articles are just markdown files
- The actual website *HTML* pages are generated using
  [*Hugo*](https://gohugo.io), a static site generator
- An open source
  [theme](https://github.com/panr/hugo-theme-hello-friend/) is used by
  the static site generator for styling the generated pages

The blog is published online through a
[*continuous delivery*](https://github.com/hfrsoussama/oussamahaff_dev/deployments/activity_log?environment=Production)
system using [*Vercel*](https://vercel.com/) which builds automatically
the website from *Github* repo `master` branch and publish it on CDN.

If you want to try the website locally, you need to :
- Install [*Hugo*](https://gohugo.io/getting-started/quick-start/)
- Clone the website's *Github* [repository](https://github.com/hfrsoussama/oussamahaff_dev/)
- Launch the command `hugo server` from the root folder of the clone repo
- In most cases, *Hugo* will indicate that the site is available locally
  on your machine at `localhost:1313`


