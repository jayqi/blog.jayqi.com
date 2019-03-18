---
title: "Setting Up Hugo and Netlify"
date: 2019-03-17T22:01:14-05:00
draft: false
---

In a [previous post]({{< ref "/posts/choosing-hugo-and-netlify" >}}), I talked about choosing to use Hugo and Netlify.

In this one, I will talk more about how I created a new Hugo blog, pushed the source code to GitHub, and built and deployed on Netlify. I'll walk through the steps I took to actually set it up a new---in particular, linking to the guides I followed. There were, unfortunately, a few gotchas that tripped me up. Hopefully this post will help someone else get through this more easily.

## Setting up a Hugo site

Follow this, but beware the gotcha below: [Hugo -- Quick Start Guide](https://gohugo.io/getting-started/quick-start/)

### Gotcha: Configuring the theme

Not too far into the guide, I got to the part of setting Ananke as the theme and figured I would just immediately use a different theme. After all, it involves cloning submodules, and I didn't really want to clone something I wasn't intending to use. Themes should be modular and easy to swap in, right?

It turns out that swapping to another theme was a little trickier than I expected. I tried two different themes, [hyde-hyde](https://themes.gohugo.io/hyde-hyde/) and [tranquilpeak](https://themes.gohugo.io/hugo-tranquilpeak-theme/) and got something that looked like this:

![hyde-hyde with no configuration](/posts-img/hyde-hyde-no-config.png)

That doesn't look nearly as good as the showcased example. Well, it turns out the [instructions](https://github.com/htr3n/hyde-hyde#installation) are a bit misleading: cloning the submodule and adding `theme = "hyde-hyde"` is _not_ all you need to do. In order to get the extra stuff, you need to configure it on your `config.toml`. Take a look at the theme's `exampleSite/config.toml` for what to copy in. (Here's [`hyde-hyde/exampleSite/config.toml`](https://github.com/htr3n/hyde-hyde/blob/master/exampleSite/config.toml).) This seems to be an omission in many themes' documentation, but the `exampleSite` also seems to be a standard thing to have.

Note that static files like images go into the `static/` directory, but they are served from the root path, so an image at `/static/img/photo.jpg` should be specified as `/img/photo.jpg`.

## Setting up on Netlify

First, make a repository on GitHub and set it as the remote for your new site. If you're not familiar with how to do that, here is [GitHub's documentation](https://help.github.com/en/articles/adding-an-existing-project-to-github-using-the-command-line).

Then, follow this guide: [Hugo -- Hosting on Netlify](https://gohugo.io/hosting-and-deployment/hosting-on-netlify/)

Once you have it set up, pushing commits to GitHub should trigger Netlify to build your site.

### Debugging broken builds

If your new site isn't working, you might have a failed build. In case you get lost on the Netlify control panel like I did, you can see build statuses and logs by going to "Deploys" in the top navbar. This will show you a list of builds, and you can click on one to see the log.

In particular, I was getting broken builds with the following error:

```
9:01:44 PM: Error: failed to prune cache "assets": remove 9:06:44 AM: Error: failed to prune cache "assets": remove /opt/build/repo/resources/_gen/assets/scss/scss/hyde-hyde.scss_4fddb88d50abca04f2e7ef77f0bb1c3b.content: no such file or directory
```

It turns out that something about my theme (hyde-hyde) and the `--gc` cleanup after building wasn't working. I had tried copying the `netlify.toml` [this blog post](https://rozgonyiova.com/posts/deploy-hugo-with-netlify/) and it ended up building successfully.
