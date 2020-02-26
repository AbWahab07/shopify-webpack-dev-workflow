# 👷🏼‍♂️ Webpack Shopify Theme Development Tool

**This Webpack config was created to replace Slate by Shopify. This workflow functions similiarly to Theme Kit but offers you the ability to use modern JavaScript and create template specific JS and CSS bundles.**

## System Requirements 🖥
- Node (Latest release)
- NPM 5+

## Getting Started 🎬
1. Download this repo and run `npm install`.
2. If starting a new theme from scratch, use [Theme Kit's 'new' command to generate a new theme on your store](https://shopify.github.io/themekit/commands/#new). After that theme has been uploaded to your store, copy the theme ID for the next step.
3. Update the `<PASSWORD>`, `THEME_ID`, and `STORE_URL` in **config.yml** with your store & theme details.
4. If migrating an existing theme, upload assets and replace liquid files with your theme's code.
5. Run `npm start` to run your first Webpack build and start watching for file changes to be uploaded to Shopify.

## Configuration ⚙️

### Webpack

#### Entry Points
All JavaScript files in the `js/bundles` directory & subdirectories are used as entry points. All other JavaScript modules should added to additional subdirectories of `js/`. An entry point file must be created for each liquid template file, including alternate templates. A CSS file for each template and layout should also be added to `styles/layout` and `styles/templates`. These CSS files should be imported at the top of each JavaScript entry file.

#### Output Files
Webpack will generate a JavaScript file for each template and layout file in the `bundles` directory. The CSS files imported in each bundle entry file will also generate CSS files. Webpack will add all output files to `dist/assets`.

### Theme Kit

#### Config
The Theme Kit configuration file uses `dist` as the root directory.

#### File Uploads
When running `npm start`, Webpack will use a plugin that runs `shopify-themekit watch` after a successful build. Webpack will then be set to watch and recompile file changes, and Theme Kit will watch for file changes in the `dist` directory.

## Required Files ‼️
- The `style-bundle.liquid` and `script-bundle.liquid` snippets output dynamic asset URLs based on current layout and template. These have been added to sample `theme.liquid`. If using Shopify Plus, render `style-bundle.liquid` in `<head>` and `script-bundle.liquid` before the closing `</body>` tag. The `layout` variable is required.
- If using Shopify Plus, render these snippets in `checkout.liquid` by changing the snippet's layout variable to `checkout`. ie. `{% render 'style-bundle', layout: 'checkout' %}`.

## Notes 📝
- Subdirectories are allowed in `assets/`, `js/`, `styles/`, `snippets/`.
- A `Styles` module alias for the styles directory is ready to use. ie. `import "Styles/layout/theme.scss"`
- A git pre-commit hook is installed that will run `webpack build` prior to the commit. This is useful if using a code deployment tool so that you never push and deploy an unbuilt theme.
- `clean-webpack-plugin` was intentionally not included to make incremental deployments faster using [Buddy](https://buddy.works/). If you remove a bundle entry file, you'll also need to delete the bundle files from `dist/assets`.