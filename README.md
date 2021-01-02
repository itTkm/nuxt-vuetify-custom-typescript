# Vuetify + Nuxt.js + Typescript template (Customized)

## Overview

This project was customized from [initial template](https://github.com/nuxt/create-nuxt-app/tree/master/packages/cna-template/template/frameworks/vuetify) that created with below settings.

```
npx create-nuxt-app nuxt-vuetify-custom
create-nuxt-app v3.2.0
✨  Generating Nuxt.js project in nuxt-vuetify-custom-typescript
? Project name: nuxt-vuetify-custom-typescript
? Programming language: TypeScript
? Package manager: Yarn
? UI framework: Vuetify.js
? Nuxt.js modules: Axios, Progressive Web App (PWA), Content
? Linting tools: ESLint, Prettier, Lint staged files, StyleLint
? Testing framework: Jest
? Rendering mode: Single Page App
? Deployment target: Static (Static/JAMStack hosting)
? Development tools: (Press <space> to select, <a> to toggle all, <i> to invert
selection)
? Continuous integration: GitHub Actions (GitHub only)
? What is your GitHub username? ittkm
? Version control system: Git
```

## What has been customized?

- Remove unnecessary code such as demo code.
- Support Typescript with [nuxt-property-decorator](https://github.com/nuxt-community/nuxt-property-decorator#nuxt-property-decorator).
- Get parameter of the application information from `package.json` then use these parameters on the code.
  - Application name on the AppBar and Content.
  - Add the author name to the footer copyright.
  - Add the application version to the right of the footer.
- Change the behavior of the navigation drawer.
  - On a wide screen such as a PC, you will always see a minimized navigation drawer. Click the hamburger icon to see the full size navigation drawer.
  - On small screens such as smartphones, the full size navigation drawer is only displayed when the hamburger icon is clicked.
- Support the theme switching with icon button on the right of AppBar.
  - Dark <-> Light
  - The settings are stored in localStorage and used for subsequent access.

## Build Setup

```bash
# install dependencies
$ yarn install

# serve with hot reload at localhost:3000
$ yarn dev

# build for production and launch server
$ yarn build
$ yarn start

# generate static project
$ yarn generate
```

For detailed explanation on how things work, check out [Nuxt.js docs](https://nuxtjs.org).

## License

This project is licensed under the [MIT License](./LICENSE).
