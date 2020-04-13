<template>

  <div id="app">
    <button class = "btn btn-lg btn-primary" @click="getStarted()">Get Started</button>
    <button class = "btn btn-lg btn-primary" @click="form()" v-if="showlistapp">Add activity</button>
    <Home v-if="false" />
    <List v-if="showlistapp" @emitDelete="deleteItem($event)"
    @rateActivity="rateActivity($event)"
    :activityList="activityList"/>
    <Form v-if="showform" :activityList="activityList"/>
    <a id="anchor"></a>
  </div>
</template>



<script>

import Vue from 'vue'
import { BootstrapVue, IconsPlugin } from 'bootstrap-vue'

Vue.use(BootstrapVue)
Vue.use(IconsPlugin)

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

    showform: false,
    showlistapp: false,
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

    },
    rateActivity(keys){
      this.activityList = this.activityList.filter((item) => {
        if( item.activity == keys.key ){
          item.score = keys.score;
          return item;
        } else{
          return item;
        }
      });
    },
    getStarted() {
      this.showlistapp = true;
      this.showform = false;


  },
    form() {
      this.showlistapp = false;
      this.showform = true;

    }

  },




}
</script>

<style>

body {

  background-image: url('./components/images/nature-pic.jpg');
  -webkit-background-size: cover;
  -moz-background-size: cover;
  background-size: cover;
  -o-background-size: cover;
  background: no-repeat;
}

*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;


}
#app {
   font-family: 'Orbitron', sans-serif, monospace;
  letter-spacing: 2px;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

  color: #2c3e50;
  background-image: url('./components/images/nature-pic.jpg');
  height: 100vh;
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  z-index: -1;

}

button{
  cursor: pointer;
}

a{
  text-decoration: none;
  cursor: default;
}
</style>
