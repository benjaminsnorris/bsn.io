---

title: Using Workflow to publish to GitHub pages
summary: Leverage the power of automation to reduce friction in publishing from anywhere
categories: process reference
date: 2017-01-05 23:47:17-0700
---

## Microblog posts
This blog is hosted using [GitHub Pages](https://pages.github.com/), which has worked out extremely well for me. However, there can sometimes be too much friction to get content published, especially short-form microblog posts. Recently, I was talking with [Manton Reece](http://manton.org/) about how to publish Instagram posts to my microblog. He mentioned that he uses [Workflow](https://workflow.is/), a fantastic automation app for iOS to take an Instagram photo and publish it to his WordPress blog. He wrote [a post](http://www.manton.org/2016/03/blogging-your-photos.html) about his process that was helpful as I looked at how to make this work for my needs. Another big help was a recent series about Workflow on [Canvas](https://www.relay.fm/canvas), a podcast about iPhone and iPad productivity.

I only recently started posting my professional content to Instagram, such as sketchnotes and drawings, and it feels like a great fit. I want to keep sharing there, but I want to make sure that I have my own record of the content I am posting as well. Using [the workflow I created](/resources/microblog-post-to-github.wflow), here are the basic steps:

- While posting to Instagram, copy the caption text to the clipboard. This will be the default text for the microblog post, although I can edit it if I want.
- Select the image in Photos, or run the workflow and select the image later.
- Choose the post date in the workflow, which defaults to the current date and time.
- Workflow creates a title for both the image and the post based on the date.
- Add an additional category to the post if I want, such as for a sketchnote post.
- Confirm the post text that Workflow creates, complete with the proper front matter for posting to GitHub.
- Workflow commits the image and, if that is successful, the text post to my blog repo using the GitHub API.
- I can choose to compose a tweet with the image and text to send if I want. Typically, I will use this when posting an image that I have not already put on Instagram, such as when sketchnoting a conference.

I am pretty excited about how simple it is. I have made the workflow so that it can be launched while sharing some text, or an image, or even directly with the image and text being selected later. This has helped reduce the friction and encourages me to post more frequently. You can still [follow me on Instagram](https://www.instagram.com/bsndesign/), but all of my posts will also be available in my [microblog](/microblog/).


## Full blog posts
After getting publishing working for microblog posts, I had to keep going. I have started most of my posts on the iPad using [iA Writer](https://ia.net/writer/), and have had to sync them over to my computer where I would post them to GitHub in order to publish them. I decided to make a few workflows so that I could do all of my publishing from my iPad, or even my iPhone. They all work similarly to the workflow for microblog posts. Here are links to download the workflows:

- [Publish Blog Post](/resources/publish-blog-post-to-github.wflow)
- [Publish Photos](/resources/publish-photos-to-github.wflow)
- [Update Blog Post](/resources/update-blog-post-on-github.wflow)
- [Publish Files](/resources/publish-files-to-github.wflow)
- [Update Files](/resources/update-files-on-github.wflow)

The update workflows will take in an existing file, and first find it on GitHub, and then commit an update to the file. Adding the workflows for photos and files means that I can publish everything that the blog post will need. These have the side benefit of being able to upload any files to a repository, so their use is not limited to GitHub Pages blogs.


## Onward
Hopefully this increased ease of publishing will help me to be more consistent with my blog. Like most things, it tends to ebb and flow with me, but I want to write more regularly.