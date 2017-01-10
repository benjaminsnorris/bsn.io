---

title: Public drafts with a GitHub Pages blog
summary: 
categories: process reference
date: 2017-01-09 20:49:55-0700
---
public-drafts-with-a-github-pages-blog



title: Public drafts with a GitHub Pages blog
summary: 
categories: process reference



I wrote [last week]({% post_url 2017-01-06-using-workflow-to-publish-to-github-pages %}) about publishing to a GitHub Pages blog using [Workflow](https://workflow.is) on the iPad. As I worked on writing that post, I realized there was one piece missing from my process: previewing the draft. When I write locally on my computer, I compile the site using the [Jekyll commands](https://jekyllrb.com/docs/usage/) and include drafts. Then I can work on a post and see how it is coming, and make sure that the links all work properly and do a final check before publishing the post. With the process I had before, a post would go straight from iA Writer to published on my site, and that made me a bit nervous.

## Displaying drafts
Jekyll [already supports drafts](https://jekyllrb.com/docs/drafts/), but the only way to see them is when building locally. As I looked into the easiest way to display drafts on my published site, I realized that I already have a model that would work well. For my [apps](/apps) and [libraries](/libraries), I am using the [collections features](https://jekyllrb.com/docs/collections/) of Jekyll. In order to extend the default functionality of drafts to work, only a few small changes are needed:

1. Add drafts collection
2. Specify default layout
3. Make an index page
4. Prevent indexing

### Add drafts collection
In your `_config.yml` file, add a few lines to enable the drafts collection:

```yml
  collections:
    drafts:
      output: true
```

### Specify default layout
Also in `_config.yml`, it is easiest to provide a default layout for all drafts. This way, you can omit the layout from the front matter of the actual post, and it will display correctly when it is a draft, as well as when you publish the post.

```yml
  defaults:
    -
      scope:
        path: ""
        type: drafts
			values:
			  layout: draft
```

### Make an index page
At this point, the individual draft pages will display correctly, but it is much easier to have a page with a list of all drafts. It can be as simple as this:

```html


layout:       page
title:        Drafts
permalink:    /drafts/
meta_robots:  noindex



<p>These are draft posts for previewing.</p>

<div class="posts">
  {% assign sorted = (site.drafts | sort: 'date') | reverse %}
  {% for draft in sorted %}
    <div class="post py2">
      <p class="post-meta h5">{{ draft.date | date: site.date_format }}</p>
      <a href="{{ draft.url }}" class="post-link"><h3 class="post-title">{{ draft.title }}</h3></a>
      {% if draft.categories.size > 0 %}
        <span class="post-meta small">
          {% for category in draft.categories %}
            <a href="{{ category }}" class="category">{{ category }}</a>
          {% endfor %}
        </span>
      {% endif %}
    </div>
  {% endfor %}
</div>
```

### Prevent indexing
You may have noticed an entry in the front matter of the drafts index page with the key `meta_robots`. I have something similar in the `draft.html` default layout:

```yml


layout: post
meta_robots: noindex


{{ content }}
```

These insert the correct metadata in the `head` using the following code:
```
    {% if page.meta_robots %}
    <meta name="robots" content="{{ page.meta_robots }}">
    {% elsif layout.meta_robots %}
    <meta name="robots" content="{{ layout.meta_robots }}">
    {% else %}
    <meta name="robots" content="all">
    {% endif %}
```

This ensures that the drafts can be posted without affecting the site adversely or having incorrect links show up in search results. It is still possible for someone to find one of these posts and link to it, which will result in a 404 after publishing, but the likelihood of that is low enough to not be a real concern.


## Add workflows
- Publish draft
- Update draft
- Publish post
- Delete files