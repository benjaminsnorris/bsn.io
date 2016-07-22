---
layout:         post
title:          Writing reusable code
date:           2016-07-05 14:10:00
summary:        Make your own life easier by focusing on writing code that you can reuse in multiple projects
categories:     process musings
---
At the beginning of this year, I was put on a new project and a new team at work. We had the chance to a build a project completely from scratch. When I joined the team, they had already spent a few months interviewing potential customers and learning about our market, and were ready to build a prototype. I was tasked with creating a quick, simple version of our app that stored all data locally. I knew that I would be rebuilding the app a couple times, or at least refactoring major portions of the app. So one focus of mine was to build portions of the app in ways that I could easily reuse them multiple times, and across multiple projects.

One thing that has made this easier is that my employer has been generous in allowing large portions of my work to be open-source. As I worked on my project, I was conscious to separate app-specific code from reusable pieces that could be made into frameworks or libraries.

One of the first areas that I tackled was to create a network stack that built on top of `NSURLSession` and provided a simple interface to make network requests. The end result is somewhat specific to our projects at O.C. Tanner, but we made it open-source: [ios-network-stack](https://github.com/octanner/ios-network-stack).

Since then, I have made a [number of libraries](/code) that I use across different apps. Most of the libraries are not to the level that I would like yet—I need to add automated tests, better code documentation, and useful readme files. But I have learned a number of things in creating and using these libraries, and thought it would be useful to go through some of the pros and cons.


## Cons

### Dependency management
For a long time, I resisted adding any dependencies to my projects. It felt much simpler to just focus on the project at hand, and build anything that was needed specific to the project. Dealing with a system such as [Cocoapods](https://cocoapods.org/) or [Carthage](https://github.com/Carthage/Carthage) felt like too much overhead. Part of my reaction came from working on projects where previous developers had pulled in so many dependencies that the project became unwieldy and difficult to update and maintain. We experimented with different approaches and finally landed on using Carthage and Git submodules, which I [wrote about earlier](({% post_url 2016-06-02-using-carthage-to-add-third-party-code %})).

Part of the key in managing dependencies reliably is being able to choose when to update those dependencies.

### Extra initial time


## Pros

### Quicker project spinup
