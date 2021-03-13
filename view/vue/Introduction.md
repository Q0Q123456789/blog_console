---
title: Introduction
date: 2021-02-20
tags:
 - vue 3.0
categories:
 -  Introduction
---

## Why Composition API?

:::tip
Note

Reaching this far in the documentation, you should already be familiar with both the basics of Vue and creating components.

:::

Creating Vue components allows us to extract repeatable parts of the interface coupled with its functionality into reusable pieces of code. This alone can get our application pretty far in terms of maintainability and flexibility. However, our collective experience has proved that this alone might not be enough, especially when your application is getting really big – think several hundred components. When dealing with such large applications, sharing and reusing code becomes especially important.

Let’s imagine that in our app, we have a view to show a list of repositories of a certain user. On top of that, we want to apply search and filter capabilities. Our component handling this view could look like this:

```` javascript
export default {
  components: { RepositoriesFilters, RepositoriesSortBy, RepositoriesList },
  props: {
    user: {
      type: String,
      required: true
    }
  },
  data () {
    return {
      repositories: [], // 1
      filters: { ... }, // 3
      searchQuery: '' // 2
    }
  },
  computed: {
    filteredRepositories () { ... }, // 3
    repositoriesMatchingSearchQuery () { ... }, // 2
  },
  watch: {
    user: 'getUserRepositories' // 1
  },
  methods: {
    getUserRepositories () {
      // using `this.user` to fetch user repositories  
    }, // 1
    updateFilters () { ... }, // 3
  },
  mounted () {
    this.getUserRepositories() // 1
  }
}

````

This component has several responsibilities:

1. Getting repositories from a presumedly external API for that user name and refreshing it whenever the user changes
2. Searching for repositories using a searchQuery string
3. Filtering repositories using a filters object

Organizing logics with component's options (data, computed, methods, watch) works in most cases. However, when our components get bigger, the list of logical concerns also grows. This can lead to components that are hard to read and understand, especially for people who didn't write them in the first place.


## Basics of Composition API

Now that we know the why we can get to the how. To start working with the Composition API we first need a place where we can actually use it. In a Vue component, we call this place the setup.

### setup Component Option