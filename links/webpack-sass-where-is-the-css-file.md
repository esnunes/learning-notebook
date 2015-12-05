Title: Webpack sass where is the css file  
Keywords: webpack, Sass  
Resource Type: link  
Resource Link: http://stackoverflow.com/questions/29210325/webpack-sass-where-is-the-css-file  

# Webpack sass where is the css file

This StackOverflow question provides instructions of how to pack `Sass` files.

At first sight when I tried to create a css bundle with Sass and CSS files I tried to use ExtractTextPlugin listing all loaders, see below:
```js
// ...
loaders: [{
  test: /\.scss$/,
  loader: ExtractTextPlugin.extract('style', 'css', 'sass'),
}],
// ...
```
The code above doesn't work, for some reason that I'm not familiar with, the css and Sass loaders must be declared together as following:
```js
// ...
loaders: [{
  test: /\.scss$/,
  loader: ExtractTextPlugin.extract('style', 'css!sass'),
}],
// ...
```
