# 👷🏼‍♂️ Webpack Shopify Theme Development Tool

**This Webpack config was created to replace Slate by Shopify. This workflow functions similiarly to Theme Kit but offers you the ability to use modern Javascript and create template specific JS and CSS bundles.**

## System Requirements
- Node (Latest release)
- NPM 5+

## Getting Started
1. Download this repo and run `npm install`.
2. Update the `<PASSWORD>`, `THEME_ID`, and `STORE_URL` in **config.yml** with your store details.
3. If migrating an existing theme, upload assets and replace liquid files with your theme's code.
4. Run `npm start` to run your first Webpack build and start watching for file changes to be uploaded to Shopify.

## Required Files
- The `style-bundle.liquid` and `script-bundle.liquid` snippets output dynamic asset URLs based on current layout and template. These have been added to sample `theme.liquid`. If using Shopify Plus, render `style-bundle.liquid` in `<head>` and `script-bundle.liquid` before the closing `</body>` tag. The `layout` variable is required.
- If using Shopify Plus, render these snippets in `checkout.liquid` by changing the snippet's layout variable to `checkout`. ie. `{% render 'style-bundle', layout: 'checkout' %}`.

## Notes
- Subdirectories are allowed in `assets/`, `js/`, `styles/`, `snippets/`.
- A `Styles` module alias for the styles directory is ready to use. ie. `import "Styles/layout/theme.scss"`
- A git pre-commit hook is installed that will run `webpack build` prior to the commit. This is useful if using a code deployment tool so that you never push and deploy an unbuilt theme.
