<template>
  <div id="app">
    <Form />
    <Home />
    <List />
  </div>
</template>

<script>

import Form from "./components/Form"
import Home from "./components/Home"
import List from "./components/List"
export default {
  name: 'App',
  components: {
    Form,
    Home,
    List
  },
  
  data: () => ({
    activityList: [
      {
        activity: "Take a walk around the house",
        category: "exercise",
        score: "3",
        source: "google"
      },
      {
        activity: "Grab a snack",
        category: "food",
        score: "3",
        source: "Fanny"
      },
      {
         activity:"powernap",
         category:"relax",
         score:"3",
         source:"computer"
      }

    ]

  })


}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
