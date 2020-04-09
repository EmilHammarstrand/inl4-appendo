<template>
  <div id="app">
    <Home />
    <List :activityList="activityList"/>
    <Form :activityList="activityList"/>
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
        tipster: "google",
        estimatedTime: "5",
        date: ""
      },
      {
        activity: "Grab a snack",
        category: "food",
        score: "3",
        tipster: "Fanny",
        estimatedTime: "7",
        date: ""
      },
      {
         activity:"powernap",
         category:"relax",
         score:"3",
         tipster:"computer",
         estimatedTime:"10",
         date: ""
      },
      {
         activity:"sleep",
         category:"relax",
         score:"3",
         tipster:"computer",
         estimatedTime:"10",
         date: ""
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
