---
layout: post
title: GraphQL. An intro.
---

It seemed to have as detractors as fans when we started evaluating whether to use GraphQL for a new project. The GraphQL tag line explains it as _a query language for your api_. But I'm not sure that really helps explain what it does & how it can help modern apps.

We ended up selecting it and now have reasonable experience with the technology. Have learnt a lot of hard lessons along the way, which I'll explain in this and a few upcoming posts.

## What is it

It's a query language or way to describe data. 

Around this language are a range of libraries and tools - eg. servers, clients, services etc. These all combine to enable an API (or query system) which decouples services & allow us to ship value. Boom! Or so it says on the box.

We've been working heavily in the JS world (React, React Native, Node), so selected the defacto standard implementation of GraphQL by [Apollo](https://www.apollographql.com). Apollo builds the popular Apollo Client and Server libraries - which have over 300,000 downloads per week.

Apollo also offer paid services on top the platform. These services are totally optional though. You can use the open source libraries for free :-) 

## Where to start

I would've like these [Principles](https://principledgraphql.com) to be around when I started with GraphQL. It could've prevented some wasted time, debate and mistakes. They're a great starting point:

- Integrity: one graph, federated & tracked in a registry. 
- Agility: build the graph up based on real needs, when needed. Just like evolutionary architecture!
- Operations: control access, layer and advanced logging.

Probably should read the [official spec](https://facebook.github.io/graphql/draft), or at least parts of it. It helps to understand what's GraphQL vs what is provided by libraries.  

## Options

While GraphQL has now been around for some time (available publicly since 2015) and it's usage is widespread, there are still plenty of detractors, misinformation and varied approaches. 

One criticism is around loosing control of how your back-end. Front end engineers writing random inefficient queries. Will you loose control of the back-end? 

To fuel that fire, there are tools like [this](https://hasura.io) which layer GraphQL directly on top of the database. They may be good for prototyping and some edge cases, but the [recommended approach](https://principledgraphql.com/operations#10-separate-the-graphql-layer-from-the-service-layer) is further separation. 

## Next

In the next few posts, I'll write up some of our lessons learnt.



