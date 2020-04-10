<template>
  <div id="app">
    <button><a href="#anchor">Add activity</a></button>
    <Home />
    <List @emitDelete="deleteItem($event)" 
    :activityList="activityList"/>
    <Form :activityList="activityList"/>
    <a id="anchor"></a>
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
        date: "2020-02-09 02:09:43"
      },
      {
        activity: "Grab a snack",
        category: "food",
        score: "3",
        tipster: "Fanny",
        estimatedTime: "7",
        date: "2019-07-21 18:02:22"
      },
      {
         activity:"powernap",
         category:"relax",
         score:"3",
         tipster:"computer",
         estimatedTime:"10",
         date: "2020-04-10 12:11:02"
      },
      {
         activity:"sleep",
         category:"relax",
         score:"3",
         tipster:"computer",
         estimatedTime:"10",
         date: "2018-12-24 23:03:43"
      }
    ]
  }),
  methods: {
    deleteItem(key){
       this.activityList = this.activityList.filter( item => item.activity != key)
         
    }
  }
  

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

a{
  text-decoration: none;
  cursor: default;
}
</style>
