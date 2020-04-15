<template>
  <div id="app">
    <div class="intro-text" id="toTop">
      <h1>AppenDo</h1>
      <p v-if="!showlistapp">Glued to the computer during break? AppenDo helps you to break FREE</p>
      <p v-if="showlistapp">Create your activity:</p>
      <button
        class="btn btn-lg btn-info getstarted"
        @click="getStarted()"
        v-if="!showlistapp"
      >Get Started</button>
    </div>


    <img src="./assets/left-arrow.svg" class = "goBackButton" @click="showlistapp = !showlistapp" v-if="showlistapp" alt="backicon">

    <a href="#formdiv-scroll">
      <button
        class="btn btn-lg btn-info add-activity"
        @click="form()"
        v-if="showlistapp"
      >Add activity</button>
    </a>

    <div class="showing-whole-form" v-if="showlistapp">
      <!-- <a href="anchor">To the bottom</a> -->

      <Home v-if="false" />

      <div>
        <List
          v-if="showlistapp"
          @emitDelete="deleteItem($event)"
          @rateActivity="rateActivity($event)"
          :activityList="activityList"
        />
      </div>


      <a href="#toTop" id="toTopButton">
        <button class="btn btn-info btn-lg">Go Back Up</button>
      </a>

      <div class="form-div" id="formdiv-scroll">
        <Form :activityList="activityList" />
      </div>

      <!-- <a id="anchor">To the Top</a> -->
    </div>
  </div>
</template>

<script>
import Form from "./components/Form";
import Home from "./components/Home";
import List from "./components/List";
export default {
  name: "App",
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
        activity: "powernap",
        category: "relax",
        score: "3",
        tipster: "computer",
        estimatedTime: "10",
        date: "2020-04-10 12:11:02"
      },
      {
        activity: "sleep",
        category: "relax",
        score: "3",
        tipster: "computer",
        estimatedTime: "10",
        date: "2018-12-24 23:03:43"
      }
    ]
  }),
  methods: {
    deleteItem(key) {
      this.activityList = this.activityList.filter(
        item => item.activity != key
      );
    },
    rateActivity(keys) {
      this.activityList = this.activityList.filter(item => {
        if (item.activity == keys.key) {
          item.score = keys.score;
          return item;
        } else {
          return item;
        }
      });
    },
    getStarted() {
      this.showlistapp = true;
      this.showform = false;
    },
    form() {
      window.scrollTo(0, 50);

      // this.showlistapp = false;
      // this.showform = true;
    }
  },
  mounted() {

    if (localStorage.length <= 1 ) {
      localStorage.setItem("activityList", JSON.stringify(this.activityList));
    }

    else if (localStorage.activityList.length==2){
      localStorage.setItem("activityList", JSON.stringify(this.activityList));
    }

    else {
      this.activityList = JSON.parse(localStorage.getItem("activityList"));
    }
  },
  updated() {
    localStorage.setItem("activityList", JSON.stringify(this.activityList));
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Quicksand&display=swap");

#app {
  font-family: "Quicksand", sans-serif;
  letter-spacing: 0.5px;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  background-image: url("./components/images/nature-edited.jpg");
  height: 100vh;
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  background-attachment: fixed;
  z-index: -1;
  overflow: auto;
}
.goBackButton {

  height: 40px;
  width: 40;
  margin-left: 20px;
  cursor: pointer;



}


.getstarted {
  margin-top: 83px;
  font-size: 1.2rem;
  width: 200px;
  height: 87px;
  animation: puff-in-center;
  animation-duration: 0.5s;
}

p {
  font-size: 1.5rem;
}

.add-activity {
  float: right;
  margin-right: 20px;
  margin-bottom: 15px;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  scroll-behavior: smooth;
}

.intro-text {
  color: white;
  text-align: center;
  padding: 30px;
  margin: 20px 0px 0px 0px;
}

.intro-text > h1 {
  font-size: 5rem;



}

.form-div {
  text-align: center;
  margin-top: 60px;
  padding-top: 20px;
}

button {
  cursor: pointer;
}

a {
  text-decoration: none;
  cursor: default;
  color: white;
  display: flow-root;
}

#toTopButton {
  float: right;
  margin-right: 20px;
  margin-top: 15px;
}



::-webkit-scrollbar-track {
  background: rgb(134, 140, 143);
}

::-webkit-scrollbar-thumb {

  background: rgb(42, 41, 41);
}


@media(max-width: 411px) {

.intro-text > h1 {
  font-size: 3rem;
}



}

@media(max-width: 320px) {

.intro-text > h1 {
  text-align: center;
  font-size: 50px;
  border: 2px solid green;
}


}



@media(max-width: 786px) {

.intro-text > h1 {
  font-size: 4rem;
}


}

/* just a test */
@keyframes puff-in-center {
  0% {
    -webkit-transform: scale(2);
            transform: scale(2);
    -webkit-filter: blur(4px);
            filter: blur(4px);
    opacity: 0;
  }
  100% {
    -webkit-transform: scale(1);
            transform: scale(1);
    -webkit-filter: blur(0px);
            filter: blur(0px);
    opacity: 1;
  }
}



</style>
