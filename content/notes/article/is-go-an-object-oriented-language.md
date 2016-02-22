---
date: 2016-02-22T18:14:00-03:00
title: Is Go an Object Oriented Language?
source: http://spf13.com/post/is-go-object-oriented/
is: Article
categories:
  - Golang
  - Object-Oriented Programming
---

This article was written by Steve Francia, the author of
[Hugo](https://gohugo.io/). Hugo is an amazing static website engine written in
[Go](https://golang.org/). As I'm in the process of learning go I decided to
look at Steve's blog posts trying to find more information about both Hugo and
Go.

The article tries to list what makes a programming language support OOP design.
It points out a brief information about OOP concepts like:

- Inheritance And Polymorphism;
- Single & Multiple Inheritance;
- Subtyping (Polymorphism);
- Object Composition

The article describes how and which of those concepts Go supports.

Steve, as most part of *modern* software development communities, considers
Inheritance as a bad practice. In order to fundament his opinion Steve quotes
James Gosling (Java's inventor) and mentions that GoF book discusses at length
replacing implementation (extends) with interface inheritance (implements).
