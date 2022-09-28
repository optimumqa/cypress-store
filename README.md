<h1 align="center">Welcome to cypress-store👋 </h1>
<a href="https://github.com/optimumqa/cypress-store/blob/main/LICENSE">
  <img alt="License: MIT" src="https://img.shields.io/badge/license-MIT-yellow.svg" target="_blank" />
</a>

[![ci](https://github.com/optimumqa/cypress-store/actions/workflows/release.yml/badge.svg?branch=main)](https://github.com/optimumqa/cypress-store/actions/workflows/release.yml)

<div align=center>

  <a href="">
    <img alt="Cypress" src="https://img.shields.io/badge/-cypress-%23E5E5E5?style=for-the-badge&logo=cypress&logoColor=058a5e" target="_blank" />
  </a>
  <a href="">
    <img alt="Javascript" src="https://img.shields.io/badge/javascript-%23323330.svg?style=for-the-badge&logo=javascript&logoColor=%23F7DF1E" target="_blank" />
  </a>

This plugin enables you to <b>store</b> and <b>share</b> values between multiple spec files

</div>

## Installation

```sh
npm install @optimumqa/cypress-store
```

## Usage

### Cypress version >= 10

```js
// ./cypress.config.js

import { defineConfig } from 'cypress'

const finalConfig = defineConfig({
  e2e: {
    setupNodeEvents(on, config) {
      // Setup plugins
      config = import('@optimumqa/cypress-store')(on, config)

      return config
    },
  },
})
```

### Cypress version < 10

```js
// ./cypress/plugins/index.js

module.exports = (on, config) => {
  config = require('@optimumqa/cypress-store')(on, config)

  return config
}
```

### Usage

Below is an example saving a token inside one spec, and re-use it inside another.

You can have infinite stores.

Example of setting a new item into 'CommonStore'.

> If the store does not exist, it will be automatically created:

```js
// mySpec1.cy.js

cy.task('setItem', {
  storeId: 'MyStoreForUsefulStuff',
  item: {
    name: 'foo',
    value: 'bar',
  },
})
```

Example of getting an item from a store:

```js
// mySpec2.cy.js

cy.task('getItem', {
  storeId: 'MyStoreForUsefulStuff',
  item: {
    name: 'foo',
  },
}).then((item) => {
  console.log(item) // { name: 'token, value: 'foo' }
  console.log(item.name) // foo
  console.log(item.value) // bar
})
```

## 🤝 Contributing

Contributions, issues and feature requests are welcome.<br />
Feel free to check [issues page](https://github.com/optimumqa/cypress-store/issues) if you want to contribute.<br />

## Show your support

Please ⭐️ this repository if this project helped you!

## 📝 License

This project is [MIT](https://github.com/optimumqa/cypress-store/blob/main/LICENSE) licensed.
