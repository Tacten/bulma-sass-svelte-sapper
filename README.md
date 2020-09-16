# Integrate sass version of Bulma with Sapper / Svelte

Follow instrucntion  [here](https://sapper.svelte.dev/docs) for installing Sapper through rollup


## Installing Bulma 
Inside you app folder
 ```
npm i -D bulma
 ```
or alternatively if you are taking of clone of this repo
just run 
 ```
 npm install
 ```
### [Follow instruction in this blog for setting up the rollup.config.js for your sapper project to understand sass version of Bulma](https://medium.com/@sean_27490/svelte-sapper-with-sass-271fff662da9)

##  1. Parse <style lang="scss"> tags

### Install few node packages

 ```
 npm i -D svelte-preprocess autoprefixer node-sass
 ```

### Modify rollup.config.js by importing

 ```
import sveltePreprocess from 'svelte-preprocess';
 ```

### Setup preprocess function
 ```
const preprocess = sveltePreprocess({

  scss: {
    includePaths: ['src'],
  },
  postcss: {
    plugins: [require('autoprefixer')],
  },
});
```
### Call preprocess function
 ```
export default {
  client: {
    plugins: [
      svelte({
        // ...
        preprocess, // <-- ADD THIS LINE
      }),
  },
  server: {
    plugins: [
      svelte({
       // ...
        preprocess, // <-- HERE TOO
      }),
    ],
  },
};
```

Now if you add lang=scss to style tag it will parse perfectly

Next you can add your global.scss and mystlyles.css as shown in the code folder style


## 2. Fix VSCode Sytax

To fix VS Code to stop highlighting all the “errors” in your style tags,  create a svelte.config.js at top level of project with:

 ```
const sveltePreprocess = require('svelte-preprocess');
module.exports = {
  preprocess: sveltePreprocess({
    scss: {
      includePaths: ['src'],
    },
    postcss: {
      plugins: [require('autoprefixer')],
    },
  }),
};git
 ```
You may also need to tell the Svelte extension the path to Node. If so, just open VS Code > Preferences > Settings and search for “svelte”. Right at the top, you should see: “Svelte > Language-server: Runtime”. You need to supply your Node path there. To get it, pop open a terminal and type which node, then copy/paste that path there. Mine is: /usr/local/bin/node but yours might be different.

## License
### MIT
