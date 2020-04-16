<template>
    <div class="activityCard">
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

          <div class="ratePart">
            <label for="score">Rate activity:</label>

            <select
              @change="updateUserScore"
              name="score"
              id="submitScore"
              @click="scoreOptionTouched=true"
            >
              <option value="1">1</option>
              <option value="2">2</option>
              <option selected="selected" value="3">3</option>
              <option value="4">4</option>
              <option value="5">5</option>
            </select>
            <button @click="rateActivity(activity.activity)" class="scoreSubmitButton" :disabled="!scoreOptionTouched">Submit</button>
            <p class="score">
              <span class="score">Score:</span>
              {{activity.score}}
              
            </p>
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
    scoreOptionTouched: false,
    userScore: 3,
    
  }),

  methods:{
    emitDelete(key) {
      this.$emit("emitDelete", key);
    },
    updateUserScore() {
      this.userScore = event.target.value;
    },
    rateActivity(key) {
      this.$emit("rateActivity", { score: this.userScore, key: key });
    }
  },

  props:{
    activity: Object
  }
}

</script>
<style scoped>
div.activityCard {
  border-bottom: 1px solid grey;
  background-color: #465f6f;
  opacity: 0.87;
  color: white;
  display: flex;
  justify-content: space-between;
  
}

div.activityCard:nth-child(odd){
  border-right: 1px solid grey;
}
p.score {
  display: inline-flex;
}


span {
  font-weight: 600;
}

label {
  margin-top: 1.5em;
  margin-bottom: 0rem;
  white-space: nowrap;
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
.optionDiv .scoreSubmitButton {
  width: 4rem;
  margin-top: 0.3rem;
  border-radius: 4px;
  border: none;
  padding: 5px;
  color: black;
  background-color: #17a2b8;
  font-weight: bold;
}
.optionDiv .scoreSubmitButton:disabled{
  background-color:grey;
  color:rgb(73, 73, 73);
  cursor: not-allowed;
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
  margin-top: 1.2em;
  /* padding: 0.5rem; */
  cursor: pointer;
}
.items{
  margin-left: 2em;
}

@media(max-width: 475px) {

    button{
        font-size: 70%;
    }

    p.score {
        display: inline-flex;
        margin-left: 0px;
    }

    .activityCard{
        display: flex;
        flex-direction: column;
    }
    div.activityCard:nth-child(odd){
        border-right: none;
    }

    .ratePart{
        display: flex;
        flex-direction: column;
    }

    .optionDiv {
        display: flex;
        width: 100%;
        flex-direction: row-reverse;
        justify-content: center;
    }
    .items{
        display: flex;
        flex-direction: column;
        align-items: center;
        margin-left: 0;
    }
}
</style>