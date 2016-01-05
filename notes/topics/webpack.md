Title: Webpack

# Webpack

#### Dynamic public path
The `publicPath` of the output entry in webpack config file can be left blank and be dynamically set in the entry point file.
```js
__webpack_public_path__ = myRuntimePublicPath

// ... rest of your application entry
```
