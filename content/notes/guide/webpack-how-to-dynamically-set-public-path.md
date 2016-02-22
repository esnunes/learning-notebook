---
date: 2016-01-05
title: "Webpack: How to dynamically set publich path"
is: Guide
categories:
  - Webpack
---

The `publicPath` of the output entry in webpack config file can be left blank and be dynamically set in the entry point file.
```js
__webpack_public_path__ = myRuntimePublicPath

// ... rest of your application entry
```
