---
layout: post
title:  "The S.P.A Argument"
date:   2020-03-31 14:36
categories: javascript
comments: true
---

There was a short debate I had with some people regarding whether SPAs are necessary based off an article on the subject.

<!--more-->

Here's the article
https://journal.plausible.io/you-probably-dont-need-a-single-page-app

>It all comes down to tradeoffs
> As with everything in programming, there isn’t a single answer in the SPA vs traditional architecture dilemma. There are cases where it makes sense to go with a SPA because you need a snappy, real-time UI. However, we should recognize that this comes at a cost to the development speed. And if a single-page app is not a requirement, we can avoid the additional complexity and move much quicker by going the traditional route.
> Picking the right architecture for the job makes a huge difference in productivity, and ultimately, success. We should aim to have both architectures in our toolbox, so we can use the optimal solution in each case.


I'm not sure if this article was a bash at JS developers, but more so debating whether 'defaulting' to SPAs is the best solution as a starting point. Why not just build your app in NodeJS/ExpressJS, thats still Javascript and I don't see anything wrong with this.

I actually have some personal experience with this in my previous company, we were rewriting a legacy app, it used to be built with Ruby on Rails but the company wanted to use PHP instead primarily because of how difficult it was to find a Rails dev (in Milton Keynes). The senior developer and myself had started at the same time, But he being the senior there had selected the tech stack: Laravel API with an Angular 2 (SPA).

Developing with Laravel was a breeze and he was already well-versed with it, but why did he go for Angular 2? Or an SPA for that matter. When I asked him, he basically said that it was 'modern' (and I wouldn't be surprised if he just wanted to learn the tech).

After two years of developing with it, he openly admitted regretting going that route when comparing to just using the Laravel framework to handle everything incl the front end, then perhaps going with the hybrid option and using VueJS to apply the rich UI interactions.

The problems we've had with Angular were error handling, guards, intercepting calls (to handle refresh tokens) to name a few. These things can go completely without when going the traditional route, Laravel would've handled that stuff for us out of the box. I personally don't regret learning Angular but I can see why my colleague says he has regrets over it, it took us substantially longer to develop anything and the question was whether it was even *necessary* for _this particular app_

The SPA route 'arguably' adds extra complexity and setup costs when compared to the traditional route and I think that was where the author of that article was getting at.
