<!--
belongs-to: webpack, CSS
-->
# Extract Text webpack Plugin

[Link](https://github.com/webpack/extract-text-webpack-plugin)

This webpack plugin groups loaders in order to store all generated content from them inside one file.

One key benefit of it is to group all `css`, `sass`, `less` generated inside one `bundle.css` file. By doing this you no longer have to wait the whole `js` file load to see the html stylized.
