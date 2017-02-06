---
title: Plugins
sort: 8
contributors:
  - sokra
  - skipjack
---

?> `plugins` customize the webpack build process in a variety of ways. This page discusses using existing plugins, however if you are interested in writing your own please visit Writing a Plugin.

## `plugins`

`array`

A list of webpack plugins. For example, when multiple bundles share some of the same dependencies, the `CommonsChunkPlugin` could be useful to extract those dependencies into a shared bundle to avoid duplication. This could be added like so:

```js
plugins: [
  new webpack.optimize.CommonsChunkPlugin({
    ...
  })
]
```

A more complex example, using multiple plugins, might look something like this:

```js
plugins: [
  // Build optimization plugins
  new webpack.optimize.CommonsChunkPlugin({ name: 'vendor', filename: 'vendor-[hash].min.js' }),
  new webpack.optimize.UglifyJsPlugin({ minimize: true, compress: { warnings: false, drop_console: false } }),
  new ExtractTextPlugin({ filename: 'build.min.css', allChunks: true }),
  new webpack.IgnorePlugin(/^\.\/locale$/, [/moment$/]),
  // Compile time plugins
  new webpack.DefinePlugin({ 'process.env.NODE_ENV': '"production"' }),
  // Webpack dev server enhancements
  new DashboardPlugin(),
  new webpack.HotModuleReplacementPlugin(),
],
```
?> Add a more detailed example
