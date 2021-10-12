# vue-components

Package including some basic vue components used in several NuxtJS/Prismic projects.

## Getting Started

### Installing

Install the package

```
npm install @leetajz/vue-components
```

We don't use webpack or similar in the package, therefor we need to transpile it in Vue/Nuxt using the following in nuxt.config.js

```
build: {
    ...
    transpile: [
       '@leetajz/vue-components'
    ],
    ...
}
```

### Usage

Include components in the package by

```
import { PrismicImage } from '@leetajz/vue-components'
```
