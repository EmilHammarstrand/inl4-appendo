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
      <div v-for="(activity, index) in sortList" 
      class="activityCard" :key="activity.activity">
        <div class="items">
          <h3>{{activity.activity}}</h3>
          <p>
            <span>Category:</span>
            {{activity.category}}
          </p>
          <p>
            <span>Tipster:</span>
            {{activity.tipster}}
          </p>
          <p>
            <span>Estimated time:</span>
            {{activity.estimatedTime}} min
          </p>
          <p class="created">
            <span class="created">Created:</span>
            {{activity.date}}
          </p>
        </div>

        <div class="optionDiv">
          <img
            @click="emitDelete(activity.activity)"
            src="../assets/trash.png"
            alt="delete"
            class="delete"
          />
          <label for="score">Rate activity:</label>

          <select
            @change="updateUserScore"
            name="score"
            id="submitScore"
            @click="scoreIsClicked(index)"
          >
            <option value="1">1</option>
            <option value="2">2</option>
            <option selected="selected" value="3">3</option>
            <option value="4">4</option>
            <option value="5">5</option>
          </select>
          <button @click="rateActivity(activity.activity)" class="scoreSubmitButton" :disabled="itemScoreDisabled[index]">Submit</button>
          <p class="score">
            <span class="score">Score:</span>
            {{activity.score}}
            {{itemScoreDisabled[index]}}
            
          </p>
          <!-- ändrat här! -->
          <!-- <p>{{scoreIsClicked}}</p> -->
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Vue from "vue";
import { BootstrapVue, IconsPlugin } from "bootstrap-vue";

Vue.use(BootstrapVue);
Vue.use(IconsPlugin);

export default {
  data: () => ({
    sortBy: "latest",
    latestActive: true,
    activityActive: false,
    categoryActive: false,
    tipsterActive: false,
    estimatedTimeActive: false,
    scoreActive: false,
    userScore: 3,
   
    
    
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
          return a - b;
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
    emitDelete(key) {
      this.$emit("emitDelete", key);
    },
    updateUserScore() {
      this.userScore = event.target.value;
    },
    scoreIsClicked(scoreIndex){

      console.log("scoreisclicked körs", scoreIndex);
      
    this.itemScoreDisabled[scoreIndex]=false;
   
    

    },
    rateActivity(key) {
      this.$emit("rateActivity", { score: this.userScore, key: key });
    }
  
  },
  mounted(){
    console.log("list/mounted, itemscoredisabled: ", this.itemScoreDisabled);
    
  },
  
  props: {
    activityList: Array,
    itemScoreDisabled:Array,
  }
}; //slut export default
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Quicksand&display=swap");
@import url("https://fonts.googleapis.com/css?family=Baloo+Paaji+2&display=swap");
* {
  font-family: "Quicksand", sans-serif;
}
div.activityCard {
  border-bottom: 1px solid grey;
  background-color: #465f6f;
  opacity: 87%;
  color: white;
  display: flex;
  justify-content: space-between;
  
}

div.activityCard:nth-child(odd){
  border-right: 1px solid grey;
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

p.score {
  display: inline-flex;
}

span {
  font-weight: 600;
}
h3 {
  padding-top: 0.5em;
  padding-bottom: 0.3em;
  margin: 0.3rem 0.3rem 0.3rem 0.5rem;
}
p {
  margin: 0.3rem 0.3rem 0.3rem 0.5rem;
  font-size: 1rem;
}
p.created,
span.created {
  font-size: 0.7rem;
}
.optionDiv {
  display: flex;
  flex-direction: column;
  width: min-content;
  padding: 0.2rem 0.2rem 0.2rem;
  align-items: center;
  justify-content: space-evenly;
  text-align: center;
  margin-right: 2em;
}

p.score,
span.score {
  padding-right: 0.6rem;
}
select {
  margin-top: 0.3rem;
}
.optionDiv > .scoreSubmitButton {
  width: 4rem;
  margin-top: 0.3rem;
  border-radius: 4px;
  border: none;
  padding: 5px;
  color: black;
  background-color: #17a2b8;
  font-weight: bold;
}
.optionDiv > .scoreSubmitButton:disabled{
  background-color:grey;
  color:rgb(73, 73, 73);
  cursor: not-allowed
}

.optionDiv select {
  width: 4rem;
  padding: 5px;
  border: 1px solid #cccccc;
  border-radius: 4px;
  resize: vertical;
  margin-top: 0.3rem;
}

img.delete {
  object-fit: scale-down;
  height: 3rem;
  padding: 0.5rem;
  cursor: pointer;
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

.items{
  margin-left: 2em;
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