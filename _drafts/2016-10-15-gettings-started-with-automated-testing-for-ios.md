---
title:          Getting started with automated testing for iOS
date:           2016-10-14 13:00:00
summary:        An introduction to the basics of protecting your future self from your current self
categories:     testing
---

I have [written before](/categories/testing) about automated testing as part of iOS development, and I plan to go into more detail. But I wanted to explain some of the basics for anyone who is completely new to the idea of automated testing.

## We are like, so immature
In general, I have found the iOS developer community to be much less mature at testing than other developers I have known. There are a number of reasons for this. With some of my friends who are Ruby developers, they have commented that without tests, there is no way to know whether their code worked at all. They do not have a client to exercise their code, so they have to write tests to make sure that they are done. With iOS development, you can easily hit `⌘R` and see what you have done in the Simulator. This leads to the largely false impression that you have tested your code, and now you “know” that it works properly.

One major complaint that I have heard from developers is that they do not want to feel like they are writing their app twice. There is a feeling that writing the automated tests are unnecessary, and extra overhead that we “just don’t have time for.” Ironically, by not taking the time to write tests, we often end up spending much more time down the road debugging problems that have crept into our app as it naturally grows.

I recently heard [Casey Liss](https://www.caseyliss.com/) give a great explanation for why automated tests can be so valuable. As your app gets more complex, it becomes increasingly challenging to arrive at the part of your app where you are currently working. Imagine that you are making a ride-sharing app, and you are working on a feature that is only triggered after a ride has been completed. Without tests, it would be extremely difficult and time-consuming to get in the needed state to exercise that part of the app.


## Different levels of testing
When I think of testing software, or when I explain the concept to people, I like to think in terms of different levels. Each of the levels are appropriate at different times, and it is valuable to understand them in order to build a toolbelt from which you can draw as needed.

### Informal manual testing
This is the most common form of testing, particularly among iOS developers. Essentially this is what you are doing when you hit `⌘R` and open the simulator. You open the app, and poke around at the area you just changed and hope to see what you are expecting. For many people, this is as far as they ever get. Hopefully there is at least some level of this testing that occurs on an actual device before putting it in the hands of customers. Sometimes you will deliver the app first to beta testers in the hopes that they will do this same level of testing and increase your confidence that releasing will not be a raging ball of support fire.

Many companies, as well as individual developers, will engage in this kind of testing before a release with the hopes of catching

## How to start

## Where to go from here
