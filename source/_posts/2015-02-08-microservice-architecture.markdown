---
layout: post
title: "Microservice Architecture"
date: 2015-02-08 01:12:47 -0600
comments: true
categories: microservice, cloud, architecture
---

Microservices are a very hot topic in the industry right now. The goal of this blog post is to help define what a Microservice is, and why you would want to use them.

# What is a Microservice?

You can think of a microservice as a mini-application that can be composed into a full application. The goal of microservices is to avoid creating monolithic applications that is hard to maintain and update. Microservice architecture is not a specification but rather a design pattern or philosophy. There has been an attempt recently to better define exactly what a microservice is. Someone I personally like to follow, Martin Fowler, has recently covered the topic of microservice architecture and I rather like his take on them. I'm going to borrow his definition and briefly cover my thoughts as well on some of these. If you like you can read [Martin Folwer's post here as well.](http://martinfowler.com/articles/microservices.html) ThoughtWorks has also posted a video (on bottom of page) of [Martin Fowler speaking on this topic.](http://www.thoughtworks.com/talks/software-development-21st-century-xconf-europe-2014) I hope you check both of these out as there are some details in them I may leave out.

# Characteristics of a Microservice Architecture

## Componentization via Services

In a traditional application we typically break our code up into libraries and such. Even in most Service-Oriented Architecture we still have tons of shared libraries between services. This can lead to still having major dependencies that can cause us to update everything together. 

## Organized around Business Capabilities

This concept to me is keeping your business capabilities together as a small domain. You do have to think differently though as one may say "well everything is part of my domain". This is the wrong approach. You need to identify what really is the same domain. A good example is if you are creating an e-commerce website the account management could be a domain while the shopping aspects are separate. One could even break the cart operations separately from the actual checkout process. 
Smart endpoints and dumb pipes

The concept here to me is that the endpoints are the brains not the pipes. As an example Enterprise Service Buses have been implemented across the industry and solve lots of problems, but in doing so they have the smarts. Microservice architecture today seems to leverage message brokers more as a transport and not as a logic. This is beneficial as the only responsibility of the message broker then is to ensure the messages are delivered. If you rely on the "bus" to do smart things and you need to make a change you have now directly created a dependency to potentially multiple services which causes ripple effects. The goal of microservices is to ensure that any one microservice can be updated without requiring changes to others.

## Decentralized Governance

Monolithic approaches have a tendency to force standardization to a single technology platform. If each Microservice truly owns the full stack, meaning they control all business logic and storage of date, then as long as you have good guidelines on how you handle some of the foundational items such as security and protocols then it should not matter what technology stack you use. Now with that said it doesn't mean that an organization can just go crazy and add one hundred new languages to their plate. My philosophy on this is you should not have more technology stacks than half the number of scrum teams you have. 

## Decentralized Data Management

I sort of mentioned this above but each service should fully own their data. That means no one updates or accesses the microservices data except for the microservice. There are a lot of ways to handle this even if you feel you need some form of a central repository. Honestly I believe there are better ways to deal with needs such as reporting and analytics where you store the data properly in multiple stores but that is a topic for another day.
## Design for Failure

To be honest this is just good practice in general. In microservice architecture or even cloud architecture you have to be prepared for any piece to fail. Your services need to be resilient and deal with failure gracefully. This can be having sort of a circuit breaker approach. Let's give an example. Imagine having a system where you write information directly to storage. For some reason storage is not available. The application needs to be able store the information somewhere else so that it can later resend the information to its final resting place. To me this is just common sense in a cloud world.

## Evolutionary Design

This by no means is the easiest of the principles to achieve in real life. The goal here is that all services should be able to be changed without direct effect on others. This means you have to follow some good decision making processes. Instead of breaking a service contract you should make it backward compatible or if necessary create a new service all together. You actually can start seeing a design flaw if every time you update microservice "A" you update microservice "B" that you are coupled. It may be the fact that you actually split the same domain and microservice "B" actually should be part of microservice "A".

# Why?

Simply put we live in a world where we have to move faster and faster to keep up with market demands. Monolithic architecture typically makes it very difficult to ship products quickly. If you have to continually do full regressions across millions and millions of lines of code you fall into a trap that slows you down. If you can make small changes quickly they add up to tons of business value rather quickly. The other benefit is your customers see the small changes and feel that you are progressing instead of stagnant. This does mean that you need to still work on automated testing to ensure you do not break things. Microservices actually make for larger complications in deployment as well as make a more complicated design which may be hard for some to follow. Really in the end it is about speed and resilience though. Microservice architecture is not for everyone or even every solution. It is yet another tool in your tool-belt to use appropriately.

# So what is next?

I am planning to post a more detailed architectural post which will include diagrams around a fictitious application. This will probably come in a few weeks as I am working on a talk around this as well as Docker. Please keep your eyes open as I will be posting more content in the coming weeks.
