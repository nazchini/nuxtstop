# Nuxtstop - for all things Nuxt.js

![nuxtstop](https://user-images.githubusercontent.com/89296394/173459979-72083395-993c-43f9-a45f-67abd8885ee1.gif)


### Things I liked about Nuxt.js

This project is my first introduction to Nuxt.js as a framework for Vue.js.

- I really liked how convenient it was to use Nuxt's file based dynamic routes feature to scaffold necessary pages/App URL routes by creating a specific file structure.
- the fetch hook gives the vue component access to the 'this' context, and is able to mutate component’s data directly.
  - It means we can set the component’s local data without having to dispatch Vuex store action or committing mutation from the page component.
  - As a result, Vuex becomes optional, but not impossible. We can still use this.$store as usual to access Vuex store if required.
- I could use the fetch hook in any Vue component to access API (instead of interacting through the store) This means easier structuring of async API calls and components.
  - With old fetch or current asyncData earlier we would have to make all different requests to different DEV endpoints and then pass them to each component that requires it as a prop. But now those components are completely encapsulated.

## What I learned

- I learned how to use $fetchState for showing nice placeholders while data is fetching on the client side
  - Thanks to $fetchState.pending provided by the fetch hook we can use this flag to display a placeholder when fetch is being called on client-side.
  - this was done using the vue-content-placeholders package by Michał Sajnóg as a plugin
- how to trigger lazy loading
  - using vue-observe-visibility package by Guillaume Chau for detecting elements in viewport with IntersectionObserver (to efficiently detect when to fetch the next page in order to use DEV API's pagination parameter)
- how to use keep-alive and activated hooks to efficiently cache API requests on pages that have already been visited
  - With the keep-alive directive, fetch will trigger only on the first page visit, after that Nuxt will save rendered components in memory, and on every subsequent visit it will be just reused from the cache.
- how to reuse the fetch hook with this.$fetch()
- how to set fetchOnServer value to control when we need to render our data on the server side or not (mostly for user generated data like comments in this project which may be spammy and we dont want them to then render serverside)
- how to handle errors from fetch hook.
  - fetch is handled at the component level, so when doing server-side rendering, the parent (virtual) dom tree is already rendered when rendering the component, therefore we cannot change it by calling $nuxt.error(...), instead we have to handle the error at the component level.
  - $fetchState.error is set in the template to handle an error, if one is thrown in the fetch hook.

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
