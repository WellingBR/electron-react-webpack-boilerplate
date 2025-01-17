<p align="center">
  <img src="https://cdn.rawgit.com/alexdevero/electron-react-webpack-boilerplate/master/docs/images/electron-react-webpack-boilerplate.png" width="135" align="center">
  <br>
  <br>
</p>

<p align="center">
  <a href="https://david-dm.org/alexdevero/electron-react-webpack-boilerplate"><img alt="Dependency Status" src="https://david-dm.org/alexdevero/electron-react-webpack-boilerplate.svg?style=flat"></a>
  <a href="https://david-dm.org/alexdevero/electron-react-webpack-boilerplate?type=dev"><img alt="devDependency Status" src="https://david-dm.org/alexdevero/electron-react-webpack-boilerplate/dev-status.svg?style=flat"></a>
  <a href="http://opensource.org/licenses/MIT"><img alt="MIT License" src="https://img.shields.io/npm/l/express.svg"></a>
  <a href="https://github.com/alexdevero/electron-react-webpack-boilerplate/releases"><img alt="Current release" src="https://img.shields.io/github/release/alexdevero/electron-react-webpack-boilerplate.svg"></a>
</p>

<p align="center">
  <a href="https://paypal.me/alexdevero" rel="nofollow"><img src="https://img.shields.io/badge/Paypal-Donate-%2300457C.svg?logo=paypal&style=flat" alt="Paypal" data-canonical-src="https://img.shields.io/badge/Paypal-Donate-%2300457C.svg?logo=buy-me-a-coffee&style=flat" style="max-width:100%;"></a>
  <a href="https://patreon.com/alexdevero" rel="nofollow"><img src="https://camo.githubusercontent.com/c1eeb70a15e52f44437076a15999bb53101157f0/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f50617472656f6e2d537570706f7274212d2532334639363835342e7376673f6c6f676f3d70617472656f6e267374796c653d666c6174" alt="Patreon" data-canonical-src="https://img.shields.io/badge/Patreon-Support!-%23F96854.svg?logo=patreon&amp;style=flat" style="max-width:100%;"></a>
  <a href="https://buymeacoffee.com/alexdevero" rel="nofollow"><img src="https://img.shields.io/badge/Coffee-Donate-%23FF813F.svg?logo=buy-me-a-coffee&style=flat" alt="buymeacoffee" data-canonical-src="https://img.shields.io/badge/Coffee-Donate-%23FF813F.svg?logo=buy-me-a-coffee&style=flat" style="max-width:100%;"></a>
</p>

## Minimal Electron, React and Webpack boilerplate

Minimal Electron, React, PostCSS and Webpack boilerplate to help you get started with building your next app.

### Table of contents

* [Install](#install)
* [Usage](#usage)
* [Add Sass](#add-sass)
* [Add TailwindcSS](#add-tailwindcss)
* [Change app title](#change-app-title)
* [Contact and Support](#contact-and-support)
* [Code of Conduct](#code-of-conduct)
* [License](#license)

### Node v14x

### Install

#### Clone this repo

```
git clone https://github.com/alexdevero/electron-react-webpack-boilerplate.git
```

#### Install dependencies

```
npm install
```
or
```
yarn
```

### Usage

#### Run the app

```
npm run start
```
or
```
yarn start
```

#### Build the app (automatic)

```
npm run package
```
or
```
yarn package
```

#### Build the app (manual)

```
npm run build
```
or
```
yarn build
```

#### Test the app (after `npm run build` || `yarn run build`)
```
npm run prod
```
```
yarn prod
```

### Add Sass

Adding Sass to boilerplate requires updating webpack configs and adding necessary loaders.

1) To `webpack.build.config.js` and `webpack.dev.config.js` add new object to `rules`:

```JavaScript
{
  test: /\.scss$/,
  use: [
    { loader: 'style-loader' },
    { loader: 'css-loader' },
    { loader: 'sass-loader' }],
  include: defaultInclude
}
```

2) Install additional loaders for sass, `sass-loader` and `node-sass`.

3) Rename all CSS file to `.scss`.


### Add TailwindCSS

If you don't want to do all these steps, you can clone [This Repository](https://github.com/Sanan4li/React-Electron-TailwindCSS-Boilerplate) and you are good to go.

Adding TainwindCSS to boilerplate requires adding all the dependencies listed on the tailwindcss website for `create react app` [Official Guide](https://tailwindcss.com/docs/guides/create-react-app). OR follow these steps

1) install `tailwindcss`, `postcss` and `autoprefixer`.

```
npm install -D tailwindcss@npm:@tailwindcss/postcss7-compat postcss@^7 autoprefixer@^9
```

2) Install `craco`.

```
npm install @craco/craco
```


3) Open `package.json` file, find `start` and `build` scripts under `scripts`.

4) Add `&& craco start` at the end  in `start` and `build` scripts. You also have to add `build-css` script to build the CSS styles using tailwindCSS. `"build-css": "npx tailwindcss build  -o src/styles/main.css",`. You can choose output folder of your own choice. Here are the three scripts after changing/adding. 

```json
"start": "cross-env NODE_ENV=development webpack serve --hot --host 0.0.0.0 --config=./webpack.dev.config.js --mode development && craco start",
    "build": "cross-env NODE_ENV=production webpack --config webpack.build.config.js --mode production && craco build",
"build-css": "npx tailwindcss build  -o src/styles/main.css",
```

5) Now, create `craco.config.js` file in your project at root of your project and add the following.

```JavaScript
module.exports = {
  style: {
    postcss: {
      plugins: [
        require('tailwindcss'),
        require('autoprefixer'),
      ],
    },
  },
}
```

6) Next, generate your tailwind.config.js file:

```
npx tailwindcss-cli@latest init
```
This will create a minimal tailwind.config.js file at the root of your project.

7) (Optional) Configure Tailwind to remove unused styles in production
In your `tailwind.config.js` file, configure the purge option with the paths to all of your components so Tailwind can tree-shake unused styles in production builds:

```JavaScript
  // tailwind.config.js
  module.exports = {
   purge: [],
   purge: ['./src/**/*.{js,jsx,ts,tsx}', './public/index.html'],
    darkMode: false, // or 'media' or 'class'
    theme: {
      extend: {},
    },
    variants: {
      extend: {},
    },
    plugins: [],
  }
```

8) Add `main.css` file in `app.js`. Make sure you choose correct path for CSS file.

```
import '../styles/main.css' 
``` 

9) You may have to run `npm install tailwindcss@latest postcss@latest autoprefixer@latest` if you face different version issues. 
10) You can also check [JIT Mode In TailwindCSS](https://tailwindcss.com/docs/just-in-time-mode#enabling-jit-mode) if you want to use Just In Time Mode.


### Change app title

This boilerplate uses [HTML Webpack Plugin](https://github.com/jantimon/html-webpack-plugin#options) to generate the HTML file of the app. Changing app title is possible only through webpack configs, `webpack.build.config.js` and `webpack.dev.config.js`. App title can be changed by adding objects of options.

In `webpack.build.config.js`:

```JavaScript
plugins: [
  new HtmlWebpackPlugin({title: 'New app title '}),// Add this (line 41)
  new MiniCssExtractPlugin({
    // Options similar to the same options in webpackOptions.output
    // both options are optional
    filename: 'bundle.css',
    chunkFilename: '[id].css'
  }),
  new webpack.DefinePlugin({
    'process.env.NODE_ENV': JSON.stringify('production')
  }),
  new BabiliPlugin()
],
```

In `webpack.dev.config.js`:

```JavaScript
plugins: [
  new HtmlWebpackPlugin({title: 'New app title '}),// Add this (line 36)
  new webpack.DefinePlugin({
    'process.env.NODE_ENV': JSON.stringify('development')
  })
],
```

## Contact and Support

I want your feedback! Here's a list of different ways to me and request help:
* Report bugs and submit feature requests to [GitHub issues](https://github.com/alexdevero/electron-react-webpack-boilerplate/issues).
<!-- * For private communications email me at foo@mail.com. -->
* And do not forget to follow [@alexdevero](https://twitter.com/alexdevero) on Twitter!

If you feel generous and want to show some extra appreciation:

[![Buy me a coffee][buymeacoffee-shield]][buymeacoffee]

[buymeacoffee]: https://www.buymeacoffee.com/alexdevero
[buymeacoffee-shield]: https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png

### Code of Conduct

[Contributor Code of Conduct](code-of-conduct.md). By participating in this project you agree to abide by its terms.

### License

MIT © [Alex Devero](https://alexdevero.com).
