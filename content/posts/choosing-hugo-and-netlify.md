---
title: "Choosing Hugo and Netlify"
date: 2019-03-17T17:26:13-05:00
draft: false
---

This weekend, I decided to reboot my blog.

I had an old blog that I had written a handful of posts in 2016 but hadn't touched since. That one was a static website built using [Jekyll](https://jekyllrb.com/) and hosted on [GitHub Pages](https://pages.github.com/). Since those posts weren't really that useful, I just tore down the whole thing to start fresh. (The content from that old blog is still on [GitHub](https://github.com/jayqi/blog.jayqi.com-old).)

In this post, I discuss my thinking behind choosing to use [Hugo](https://gohugo.io/) as a site generator and [Netlify](https://netlify.com) to host. A [followup post]({{< ref "/posts/setting-up-hugo-and-netlify" >}}) walks through what I did to actually set this thing up.

## Choosing a static generator: Hugo

I had the idea early in the process this weekend that I wanted to revisit using Jekyll---I didn't really remember how it worked anyways, and I vaguely remembered dealing with Ruby being a pain given that it was and still would be the only Ruby project I have.

I knew I did still want to continue using a static site generator for two main reasons: the first being that I could write posts in Markdown, and the second being that I could host the site for free on something like GitHub pages again.

The options I considered were:

- [Jekyll](https://jekyllrb.com/)
- [Hugo](https://gohugo.io/)
- [Hexo](https://hexo.io/)
- [Pelican](https://docs.getpelican.com/en/stable/)

The first three appeared to be the most popular options for statically-generated blogs nowadays. I threw in Pelican for good measure because I am a data scientist and know how to use Python, and not so much Ruby, Go, or Node.js.

My main criterion going in was that I don't want to spend a ton of time tinkering to get the blog to work, since I didn't have a good historical track record of actually maintaining my old blog with content. Therefore:

- Simpler is better.
- Documentation needs to be good enough so I don't get stuck making it work.
- My choice mainly just needs to be good enough, because I don't want to spend a lot of time in analysis paralysis.

I ended up picking Hugo for a few reasons:

- Hugo is distributed as a single executable, so I don't need to deal with dependencies for previewing locally
- It's the next most popular after Jekyll, and my expectation is that the support and documentation will be _good enough_.
    - Hexo's community has a significant fraction that communicates in Chinese, and I need English documentation
    - Pelican didn't feel widely used enough
- Hugo is _not_ extendable with plugins but has a lot of the main features built-in. Jekyll is meant to be supplemented from a rich environment of plugins. I don't want to spend to much time tinkering (given my historical non-propensity for blogging), so
- As a data scientist, I have an eye on R community. The popular blogdown package recommends Hugo by default, and it's also what the developer Yihui Xie uses for his blog.

I want to note that one of Hugo's marketed advantages over Jekyll is that it builds really fast for large sites, compared to Jekyll. I frankly didn't really care about this, because again, I don't have high confidence I'll be writing that much.

I also want to note that only Jekyll has built-in GitHub Pages support for automatic build and deploy. I figured at first that I could copy [a Travis CI setup](https://axdlog.com/2018/using-hugo-and-travis-ci-to-deploy-blog-to-github-pages-automatically/) to do the same for Hugo. I ended up going with Netlify instead (see next section) which made this point moot.

Here are some of the things I read while investigating:

- ["An Introduction to Static Site Generators"](https://medium.com/@alexsanchezdesigns/an-introduction-to-static-site-generators-a75ab6149285)
- ["How to Choose the Right Static Generator: Jekyll vs. Hugo vs. Hexo"](https://www.techiediaries.com/jekyll-hugo-hexo/)
- ["Hugo or Jekyll? 6 Factors You Should Know"](https://forestry.io/blog/hugo-and-jekyll-compared/)
- ["Migrating Blogs (Again) from Pelican to Hugo"](https://arunrocks.com/moving-blogs-pelican-to-hugo/)
- ["The top 10 SSGs of 2018, according to StaticGen and GitHub"](https://www.netlify.com/blog/2018/08/24/the-top-10-ssgs-of-2018-according-to-staticgen-and-github/)
- ["Why I do not like Hugo"](https://flameeyes.blog/2017/07/12/why-i-do-not-like-hugo/) (this one mostly about RSS).

### Aside: Medium

I also considered using [Medium](https://medium.com/) instead. Medium would be less complicated to set up and has a network that would bring more readers. I ended up not using Medium for a few reasons:

- I wanted to be able to author my content in Markdown
- Static sites are less sticky than Medium's platform (I can take my plaintext Markdown files and do whatever in the future)
- I can always crosspost in the future if I decided I cared about the Medium network. It seemed like [internet people](https://news.ycombinator.com/item?id=13325546) recommended using a static site generator and then crossposting the content to Medium if I cared about taking advantage of the Medium network.


## Choosing hosting: Netlify

I started the morning fully intending to use [GitHub Pages](https://pages.github.com/), which was something I was familiar with. I didn't even know what Netlify was, though I had at least seen some Netlify subdomains around the R community before.

As I was reading more about setting up blogs with Hugo, I encountered more and more things talking about Netlify. In particular, I found [this blog post](https://yihui.name/en/2017/06/netlify-instead-of-github-pages/) by R developer Yihui Xie recommending Netlify over GitHub pages.

So, I chose Netlify because:

- It still deploys from GitHub (or other Git hosts), so my source content is [still on GitHub](https://github.com/jayqi/blog.jayqi.com/)
- It's [free offerings](https://www.netlify.com/pricing/) seem good enough. In particular, I can use it with my custom subdomain.
- It has rich [continuous deployment](https://www.netlify.com/docs/continuous-deployment/) supporting many static site generators, including Hugo
- It has a free [content management system (CMS)](https://www.netlifycms.org/)  with an editor that seems pretty good ([Demo](https://cms-demo.netlify.com/#/collections/posts)).
- It seems to be a widely trusted host, with many people writing about using it over GitHub Pages, including

There seem to be other bells and whistles that Netlify has that I probably won't use immediately, like HTTPS with Let's Encrypt and its own DNS and CDN (I am already using CloudFlare), but might look into more in the future. But for now it seems to be an improvement over GitHub Pages.

---

So... :tada:---here is my new blog. Here's hoping that I keep it going this time.
