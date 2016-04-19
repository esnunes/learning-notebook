---
title: "LeftPad and Go: can tooling help?"
date: 2016-04-19
is: Article
categories:
  - Golang
  - Nodejs
  - AST
source: https://divan.github.io/posts/leftpad_and_go/
---

Nice article about the mindset of Golang community regarding DRY.

> A little copying is better than a little dependency.

The article also promotes a simple tool created by the author to identify small
dependencies, [DepsCheck](https://github.com/divan/depscheck). The tool was the
first contact of the author with Golang AST (Abstract Syntax Tree), in the
article he describes how pleasant was to deal with
`go/{ast,parser,types,loader}` packages. The whole tool was the work of a 
weekend.

