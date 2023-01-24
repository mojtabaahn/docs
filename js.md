```js
# disable nuxt watching node_modules
# https://journal.simondepelchin.be/2019/07/18/how-to-ignore-node_modules-when-running-the-watcher-in-laravel-mix-nuxt-js/
# nuxt.config.js
module.exports = {
  mode: 'spa',
  
  watchers: {
    webpack: {
      ignored: /node_modules/
    }
  }
}
```
