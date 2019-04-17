---
layout: post
title: Starting and Engineering culture
---

Over the past year I've been lucky enough to co-found a startup and build a range of products from scratch. While I've built many products from scratch, my previous and most recent role was at the other end of the spectrum - with a mature company and products.

![image]({{ site.baseurl }}/images/sushobhan-badhai-372964-unsplash-2.jpg)
*Photo by Sushobhan Badhai on Unsplash*

It's given me a great opportunity to think about what's important to do when starting out. What decisions you can do early that will pay off later, what I've seen worked well, what didn't work as well or wished we'd done differently. 

There are a range of obvious decisions which I won't touch on - eg. lean/agile processes, modern architectures, platforms, CI/CD, monitoring, analytics etc. Instead, will try to cover some less obvious decisions.

1. Table of contents
{:toc}

## Conscious trade-offs

Should you write comprehensive unit tests for all code? Even if it is experimentation or prototyping and might not be released? 

When should you worry about scaling? Does performance matter when you don't know what load to expect?

Does this UI need to be a pixel perfect match to the design? Is it likely the design will change once customers start to use it?

Juggling trade-offs are hard. But it's our job to make these decisions. There's no perfect answer, and the answer is likely to change over time as knowledge improves and the product matures. But, it's easy for the answers to become cultural and questions stop being asked. Everything is done in the same way - regardless of whether it's appropriate. Misalignment between teams starts to creep in, as expectations and understanding is different.

What worked well for us was to ask these questions up front. Bake them into each story or feature and make sure everyone knows the tradeoffs and why.  

## Constantly attack technical debt

Tech debt is the cost of future rework by taking shortcuts - not to be confused with plain bad code!

If you haven't worked on a green fields project recently, you may think it takes some time before tech debt accumulates. But, unless you have the luxury of time and know ***everything***, ***exactly*** - there will be rework. We learn along the way. About the technology, platforms, services, market and customers. 

If we know tech debt is always accumulating, we should regularly pay it down. Not holding off and scheduling dedicated time in the future. In my experience, that future time will never arrive. Like paying off your mortgage, it's best if you chip away paying weekly or monthly. Prioritise debt as part of each sprint.

All tech debt isn't created equally, it has different interest rates. 

Some of it has a high interest rate - like credit card debt - and is expensive to maintain. Finance #101 says pay off your high interest debt first. These are the items slowing the team down or causing issues. 

 Other debt may have a lower interest rate and is cheaper to maintain. This debt may not be slowing the teams down or causing as many issues. Address this second. 

Scheduling a percentage of every sprint to addressing tech debt keeps it under control. The other approach I like is the "boy scout rule" - leave the campground cleaner than you found it. Made popular by Uncle Bob, whenever anyone touches something, make it better. Clean up the code, rename variables, add tests, do whatever improves it. Even if it's only picking up one empty beer can or a bottle cap next to the campfire.

## Architect for change

Software architecture can be defined as the parts that are hard to change. They are a combination of factors - performance, security, scalability, requirements, data, compliance, and all “-ilities”. 

It's sometimes easy to know which areas that are likely to change. They're the areas you know the least about. The areas that are most unknown - from either a product feature or a technology point of view. 

I've also found the need to balance architectural design with a bias for action. When there are unknowns, it's easy to over think and spend a lot of time guessing without improving outcomes. Make the best decision you can with the information at hand, within a *reasonable* time frame and that is *reasonably* easy to change in the future.

I'm also a big believer in writing only the code you need to write. Leverage as many services & standard libraries as possible.

## Define Done

Set a baseline early of what is done. Does it include tests, logging, monitoring, analytics? How about documentation and new feature announcements? Is releasing a feature enough, or does it need to be used - and what type of usage? 

It's easy for steps to be forgotten, and teams to get out of sync. Writing down these expectations helps everyone stay on the same page.

## Culture of shipping

There appears to be a natural tendency in software for *everything* to grow. 

Executives, project sponsors & product teams tend to increase scope. Engineering teams can struggle to break up tasks into smaller pieces and start to deliver less frequently in larger chunks. Pull request size increases, making it harder to review the changes. Risk increases.

We know from Lean & Agile: batch size impacts delivery and increases risk. The larger the batch the more risk. I've noticed without external forces, batch sizes tend to increase and shipping slows down.

Create a culture that breaks up tasks, values iteration and rewards shipping.

## Balance change and stability

A lot has been written about the time it takes teams to perform and deliver results. For example, [Tuckman's](https://en.wikipedia.org/wiki/Tuckman's_stages_of_group_development) forming, storming, norming & performing phases made popular by Lean & Agile.

![image]({{ site.baseurl }}/images/tuckman-team-phases.png)

We want to protect teams to ensure they reach the performing phase. But, there are challenges with too much stability. 

> Stability is also the default state. 

Beneficial team change requires work. Managers don't like loosing their good people; people tend to prefer stability.  

With stability, teams can start to optimise locally, serving their own interests over the wider group. Or begin to lack diversity in thought - and not search for improvements or challenge preconceived ideas. 

We start to see tribalism creep in, where teams protect their patch. I've also seen conflict between teams, as teams understand their own situation but have little empathy or understanding of other teams challenges. 

Team stability also creates narrow experts. Early on having experts is great, makes routing issues easy. But it creates risk - relying on individuals and is hard to scale.  

The ideal solution is to create a culture that expects some change, but not too much. Where teams are able to handle change and still perform. It's difficult to balance and I've been caught out at both ends. 

## Diversity

We all know [diversity](https://www.mckinsey.com/business-functions/organization/our-insights/why-diversity-matters) helps companies and teams. 

A few years ago I caught myself complaining about lack of gender diversity in my teams. While working towards addressing this, I lost track of other diversity planes. 

During a high growth phase the business preferred *people that can hit the ground running*. We were also hiring for individuals with a strong cultural fit. We ended up bringing on a number of very similar people and forgot about all the other diversity planes: background, age, education, seniority, experience, skills. 

A similar issue occurred with our referrals. Generally referrals are great by reducing some unknowns, but have limits, as people tend to refer alike people.

Set your diversity goals early and monitor. It's far easier to create diversity when teams are small, than to retrofit into larger teams. 

## Summary

When you're small and nimble it's easier to change direction, adjust culture and fix issues. It's the perfect time to start an engineering culture that delivers quality and produces real value.

While not a comprehensive list of items, these items have definitely helped me.