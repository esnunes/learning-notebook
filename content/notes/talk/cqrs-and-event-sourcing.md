---
date: 2016-01-29
title: Greg Young - CQRS and Event Sourcing - Code on the Beach 2014
is: Talk
source: https://www.youtube.com/watch?v=JHGkaShoyNs
categories:
  - CQRS
  - Event Sourcing
---

Very nice talk about event sourcing and how it is related to CQRS pattern.

The whole idea of storing events for future playback is awesome. You can't get
away of all pain points mentioned by Greg when it comes to move from Data
model to Event sourcing because you will be ending up querying your data
model (projections) instead of your event list, however in case something
goes wrong and you loose data, or even if you want to infer some data based
on events of the past you still have your immutable event sourcing storage.

One of the key issues of event sourcing, in my opinion, is how to deal with
changes in the event structure. During the *open for questions* part of the
presentation Greg is asked about this and he points out to a video which is
supposed to be hosted in *http://dddcqrs.com* but this url no longer exists.
After some searches on google I found out this video [here](http://www.viddler.com/v/dc528842) and [here](https://youtu.be/whCk1Q87_ZI?t=4h23m46s). The first website adds some marks to the video and there is a special mark related to **versioning** at `263:00` minutes.
