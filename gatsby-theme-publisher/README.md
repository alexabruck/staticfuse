<p align="center">
  <a href="https://www.gatsbyjs.org">
    <img alt="Gatsby" src="../gatsby-theme-tailwindcss_logo.svg" width="180" />
  </a>
</p>
<h1 align="center">
  Gatsby Tailwind Theme
</h1>

A Gatsby theme to use tailwindcss.

[Demo site](https://gatsby-theme-tailwindcss.netlify.com/)

## Summary

This theme installs:

- [Tailwindcss](https://tailwindcss.com)
- [gatsby-plugin-postcss](https://www.gatsbyjs.org/packages/gatsby-plugin-postcss/)
- [Emotion (CSS in JS)](https://emotion.sh)

Tailwindcss and postcss are required to have tailwind properly working, emotion is installed because it is very common to use a CSS in JS framework and I think it is useful to have emotion and tailwind installed and configured to work together.

## Installation

### Manually add to your site

```sh
npm install --save gatsby-theme-tailwindcss
```

or

```sh
yarn add gatsby-theme-tailwindcss
```

## Usage

### Add Tailwind to your CSS

As stated on its [official documentation](https://tailwindcss.com/docs/installation#2-add-tailwind-to-your-css), inject Tailwind's styles using the `@tailwind` directive:

```css
@tailwind base;

@tailwind components;

@tailwind utilities;
```

You should write this 3 directives either on a css you are importing or creating a new `.css` file and importing it.

I recommend creating a `globals.css` file for example in a `utils` folder and use it for tailwind loading directives and later [**extracting CSS components**](https://tailwindcss.com/docs/extracting-components#extracting-css-components-with-apply) and / or other customisations if needed.

```
├── gatsby-config.js
├── node_modules
├── package.json
└── src
    ├── pages
    │   └── index.js
    └── utils
        └── globals.css
```

**NOTE**: If you experiment a FOUC (flash of unstyled content) when first loading pages, import the above mentioned `.css` file on `gatsby-browser.js`, like this:

```js
//gatsby-browser.js
import "./src/utils/globals.css"
```

### Configuration

Add a `tailwind.config.js` file at the root of your project folder in order to use the [tailwind.macro](https://github.com/bradlc/babel-plugin-tailwind-components/releases/tag/v1.0.0-alpha.2) for CSS in JS and to be able to [customise](https://tailwindcss.com/docs/configuration) the tailwind base styles and modifiers.

```sh
yarn tailwind init
```

or

```sh
npx tailwindcss init
```

### Theme options

This theme is using [gatsby-plugin-postcss](https://www.gatsbyjs.org/packages/gatsby-plugin-postcss/) under the hood, so you can pass in any options you would to the actual postcss plugin (postCssPlugins and cssLoaderOptions)

    NOTE: using a postcss.config.js file is not supported, you have to use the options: {} object of the theme.

| Key                | Default value            | Description                            |
| ------------------ | ------------------------ | -------------------------------------- |
| `postCssPlugins`   | [require("tailwindcss")] | postcss-plugins to load                |
| `cssLoaderOptions` | {}                       | postcss css loader options             |
| `emotionOptions`   | {}                       | emotion `babel-plugin-emotion` options |

#### Example usage

The only plugin included as default is the actual tailwindcss required to work, but I do recommend using the autoprefixer plugin too.

```js
// gatsby-config.js
module.exports = {
  plugins: [
    {
      resolve: `gatsby-theme-tailwindcss`,
      options: {
        postCssPlugins: [require("autoprefixer")],
      },
    },
  ],
}
```
