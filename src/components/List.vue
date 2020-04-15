<template>
  <div class="root y">
    <div class="sortButtons">
      <button :class="latestIsActive" @click="sortByThis('latest')">Latest</button>
      <button :class="activityIsActive" @click="sortByThis('activity')">Activity</button>
      <button :class="categoryIsActive" @click="sortByThis('category')">Category</button>
      <button :class="tipsterIsActive" @click="sortByThis('tipster')">Tipster</button>
      <button :class="estimatedTimeIsActive" @click="sortByThis('estimatedTime')">Time</button>
      <button :class="scoreIsActive" @click="sortByThis('score')">Score</button> 
    </div>

    <div class="scroll-list">
      <Listitem v-for="activity in sortList" :key="activity.activity" :activity="activity"
      @rateActivity="rateActivity($event)"
      @emitDelete="deleteItem($event)"/>
    </div>
  </div>
</template>

<script>
import Vue from "vue";
import { BootstrapVue, IconsPlugin } from "bootstrap-vue";
import Listitem from "./Listitem";

Vue.use(BootstrapVue);
Vue.use(IconsPlugin);

export default {
  components:{
    Listitem
  },
  data: () => ({
    sortBy: "latest",
    latestActive: true,
    activityActive: false,
    categoryActive: false,
    tipsterActive: false,
    estimatedTimeActive: false,
    scoreActive: false,
  }),
  computed: {
    latestIsActive() {
      return this.latestActive ? "activeClass" : "";
    },
    activityIsActive() {
      return this.activityActive ? "activeClass" : "";
    },
    categoryIsActive() {
      return this.categoryActive ? "activeClass" : "";
    },
    tipsterIsActive() {
      return this.tipsterActive ? "activeClass" : "";
    },
    estimatedTimeIsActive() {
      return this.estimatedTimeActive ? "activeClass" : "";
    },
    scoreIsActive() {
      return this.scoreActive ? "activeClass" : "";
    },

    sortList() {
      let copy = [...this.activityList];

      if (this.sortBy == "latest") {
        copy.sort((a, b) => {
          if (a.date < b.date) {
            return -1;
          } else if (a.date > b.date) {
            return 1;
          } else {
            return 0;
          }
        });
        return copy.reverse();
      }
      if (this.sortBy == "activity") {
        copy.sort((a, b) => {
          if (a.activity.toLowerCase() < b.activity.toLowerCase()) {
            return -1;
          } else if (a.activity.toLowerCase() > b.activity.toLowerCase()) {
            return 1;
          } else {
            return 0;
          }
        });
        return copy;
      }
      if (this.sortBy == "category") {
        copy.sort((a, b) => {
          if (a.category.toLowerCase() < b.category.toLowerCase()) {
            return -1;
          } else if (a.category.toLowerCase() > b.category.toLowerCase()) {
            return 1;
          } else {
            return 0;
          }
        });
        return copy;
      }
      if (this.sortBy == "tipster") {
        copy.sort((a, b) => {
          if (a.tipster.toLowerCase() < b.tipster.toLowerCase()) {
            return -1;
          } else if (a.tipster.toLowerCase() > b.tipster.toLowerCase()) {
            return 1;
          } else {
            return 0;
          }
        });
        return copy;
      }
      if (this.sortBy == "estimatedTime") {
        copy.sort((a, b) => {
          return a.estimatedTime - b.estimatedTime;
        });
        return copy;
      }
      if (this.sortBy == "score") {
        copy.sort((a, b) => {
          if (a.score > b.score) {
            return -1;
          } else if (a.score < b.score) {
            return 1;
          } else {
            return 0;
          }
        });
        return copy;
      }

      return copy;
    } //slut sortlist
  }, //slut computed
  methods: {
    sortByThis(sortThis) {
      this.sortBy = sortThis;
      if (sortThis == "activity") {
        this.latestActive = false;
        this.activityActive = true;
        this.categoryActive = false;
        this.tipsterActive = false;
        this.scoreActive = false;
        this.estimatedTimeActive = false;
      } else if (sortThis == "category") {
        this.latestActive = false;
        this.activityActive = false;
        this.categoryActive = true;
        this.tipsterActive = false;
        this.scoreActive = false;
        this.estimatedTimeActive = false;
      } else if (sortThis == "tipster") {
        this.latestActive = false;
        this.activityActive = false;
        this.categoryActive = false;
        this.tipsterActive = true;
        this.scoreActive = false;
        this.estimatedTimeActive = false;
      } else if (sortThis == "estimatedTime") {
        this.latestActive = false;
        this.activityActive = false;
        this.categoryActive = false;
        this.tipsterActive = false;
        this.scoreActive = false;
        this.estimatedTimeActive = true;
      } else if (sortThis == "score") {
        this.latestActive = false;
        this.activityActive = false;
        this.categoryActive = false;
        this.tipsterActive = false;
        this.scoreActive = true;
        this.estimatedTimeActive = false;
      } else {
        this.latestActive = true;
        this.activityActive = false;
        this.categoryActive = false;
        this.tipsterActive = false;
        this.scoreActive = false;
        this.estimatedTimeActive = false;
      }
    },
      deleteItem(key) {
        this.$emit("emitDelete", key);
    },
      rateActivity(event) {
        this.$emit("rateActivity", event);
    }

  
  },
  
  props: {
    activityList: Array
  }
}; //slut export default
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Quicksand&display=swap");
@import url("https://fonts.googleapis.com/css?family=Baloo+Paaji+2&display=swap");
* {
  font-family: "Quicksand", sans-serif;
}


.scroll-list {
  overflow-y: scroll;
  max-height: 750px;
  min-height: 250px;
  border-bottom-left-radius: 15px;
  display: grid;
  grid-template-columns: 1fr 1fr;
  background-color: #465f6f;
  opacity: 87%;
  border-bottom-left-radius: 25px;
  border-bottom-right-radius: 25px;
}

.scroll-list::-webkit-scrollbar {
  width: 0px;
  background: transparent;
}



.sortButtons {
  display: flex;
  width: 100%;
}

.sortButtons > button {
  background-color: #96bb53;
  padding: 0.5em;
  border: 1px solid rgba(117, 114, 114, 0.185);
  width: 16.66%;
  opacity: 95%;
  /*border-radius:0.5em;*/
}

.sortButtons > .activeClass {
  background-color: #efc748;
}

::-webkit-scrollbar {
  width: 5px;
}

::-webkit-scrollbar-track {
  background: rgba(70, 95, 111, 0.87);
}

::-webkit-scrollbar-thumb {
  background: rgb(61, 60, 60);
}

@media (max-width: 950px) {

  .scroll-list {
  grid-template-columns: 1fr;
}

}

@media(max-width: 540px) {

  button{
    font-size: 70%;
  }

  .sortButtons > button {
    padding-top: 1em;
    padding-bottom: 1em;
    font-weight: bold;
  }

}

.y {
  display: flex;
  flex-direction: column;
  width: 90vw;
  margin: 0 auto;
}


/* @media (max-width: 769px) {
  .sortButtons > button {
    background-color: #96bb53;
    padding: 0.5em;
    font-size: 12px;
    border: 1px solid white;
    width: 16.3%;

  }
} */


/* @media (max-width: 1025px) {
  .sortButtons > button {
    background-color: #96bb53;
    padding: 0.5em;
    border: 1px solid white;
    width: 16.34%;

  }
}
*/
</style>