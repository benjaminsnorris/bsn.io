---

title: Public drafts with a GitHub Pages blog
summary: 
categories: process reference
date: 2017-01-09 21:43:24-0700
---


I wrote [last week]({% post_url 2017-01-06-using-workflow-to-publish-to-github-pages %}) about publishing to a GitHub Pages blog using [Workflow](https://workflow.is) on the iPad. As I worked on writing that post, I realized there was one piece missing from my process: previewing the draft. When I write locally on my computer, I compile the site using the [Jekyll commands](https://jekyllrb.com/docs/usage/) and include drafts. Then I can work on a post and see how it is coming, and make sure that the links all work properly and do a final check before publishing the post. With the process I had before, a post would go straight from iA Writer to published on my site, and that made me a bit nervous.

## Displaying drafts
Jekyll [already supports drafts](https://jekyllrb.com/docs/drafts/), but the only way to see them is when building locally. As I looked into the easiest way to display drafts on my published site, I realized that I already have a model that would work well. For my [apps](/apps) and [libraries](/libraries), I am using the [collections features](https://jekyllrb.com/docs/collections/) of Jekyll. In order to extend the default functionality of drafts to work, only a few small changes are needed:

1. Add drafts collection
2. Specify default layout
3. Make an index page
4. Prevent indexing

### Add drafts collection
In your `_config.yml` file, add a few lines to enable the drafts collection:

{% gist benjaminsnorris/1248c19efce6da007d5017d7b3cfaf1e _config-collections.yml %}


### Specify default layout
Also in `_config.yml`, it is easiest to provide a default layout for all drafts. This way, you can omit the layout from the front matter of the actual post, and it will display correctly when it is a draft, as well as when you publish the post.

{% gist benjaminsnorris/1248c19efce6da007d5017d7b3cfaf1e _config-defaults.yml %}


### Make an index page
At this point, the individual draft pages will display correctly, but it is much easier to have a page with a list of all drafts. It can be as simple as this:

{% gist benjaminsnorris/1248c19efce6da007d5017d7b3cfaf1e draft.html %}


### Prevent indexing
You may have noticed an entry in the front matter of the drafts index page with the key `meta_robots`. I have something similar in the `draft.html` default layout:

{% gist benjaminsnorris/1248c19efce6da007d5017d7b3cfaf1e draft-layout.html %}

These insert the correct metadata in the `head` using the following code:

{% gist benjaminsnorris/1248c19efce6da007d5017d7b3cfaf1e head.html %}

This ensures that the drafts can be posted without affecting the site adversely or having incorrect links show up in search results. It is still possible for someone to find one of these posts and link to it, which will result in a 404 after publishing, but the likelihood of that is low enough to not be a real concern.


## Add workflows
- Publish draft
- Update draft
- Publish post
- Delete files