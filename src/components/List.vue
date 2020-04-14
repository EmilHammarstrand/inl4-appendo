<template>
    <div class="root">

        <div class="sortButtons">
            <button :class="latestIsActive" @click="sortByThis('latest')">Latest</button>
            <button :class="activityIsActive" @click="sortByThis('activity')">Activity</button>
            <button :class="categoryIsActive" @click="sortByThis('category')">Category</button>
            <button :class="tipsterIsActive" @click="sortByThis('tipster')">Tipster</button>
            <button :class="estimatedTimeIsActive" @click="sortByThis('estimatedTime')">Time</button>
            <button :class="scoreIsActive" @click="sortByThis('score')">Score</button>
        </div>

        <div v-for="activity in sortList" class="activityCard" :key="activity.activity">
            <div>
                <h3>{{activity.activity}}</h3>
                <p> <span>Category:</span>  {{activity.category}}</p>
                <p> <span>Tipster:</span>  {{activity.tipster}}</p>
                <p> <span>Estimated time:</span>  {{activity.estimatedTime}} min</p>
                <p class="created"><span class="created">Created: </span>{{activity.date}}</p>
            </div>

            <div class="optionDiv">
                <img @click="emitDelete(activity.activity)" src="../assets/garbage.png" alt="delete" class="delete">
                <label for="score">Rate activity: </label>



                <select @change="updateUserScore" name="score" id="submitScore">
                    <option value="1">1</option>
                    <option value="2">2</option>
                    <option selected="selected" value="3">3</option>
                    <option value="4">4</option>
                    <option value="5">5</option>
                </select>
                <button @click="rateActivity(activity.activity)">Submit</button>
                <p class="score"> <span class="score">Score: </span> {{activity.score}}</p>
            </div>
        </div>

    </div>
</template>

<script>

import Vue from 'vue';
import { BootstrapVue, IconsPlugin } from 'bootstrap-vue';

Vue.use(BootstrapVue)
Vue.use(IconsPlugin)

export default {
    data: () => ({

        sortBy: "latest",
        latestActive: true,
        activityActive: false,
        categoryActive: false,
        tipsterActive: false,
        estimatedTimeActive: false,
        scoreActive: false,
        userScore: 3

    }),
    computed:{
        latestIsActive(){
            return this.latestActive ? "activeClass" : "";
        },
        activityIsActive(){
            return this.activityActive ? "activeClass" : "";
        },
        categoryIsActive(){
            return this.categoryActive ? "activeClass" : "";
        },
        tipsterIsActive(){
            return this.tipsterActive ? "activeClass" : "";
        },
        estimatedTimeIsActive(){
            return this.estimatedTimeActive ? "activeClass" : "";
        },
        scoreIsActive(){
            return this.scoreActive ? "activeClass" : "";
        },


        sortList(){

            let copy = [...this.activityList];

            if(this.sortBy == "latest"){
                copy.sort( (a,b) => {
                    if(a.date < b.date){
                        return -1;
                    } else if(a.date > b.date){
                        return 1;
                    } else {
                        return 0;
                    }
                })
                return copy.reverse();
            }
            if(this.sortBy == "activity"){
                copy.sort( (a,b) => {
                    if(a.activity.toLowerCase() < b.activity.toLowerCase()){
                        return -1;
                    } else if(a.activity.toLowerCase() > b.activity.toLowerCase()){
                        return 1;
                    } else {
                        return 0;
                    }
                })
                return copy
            }
            if(this.sortBy == "category"){
                copy.sort( (a,b) => {
                    if(a.category.toLowerCase() < b.category.toLowerCase()){
                        return -1;
                    } else if(a.category.toLowerCase() > b.category.toLowerCase()){
                        return 1;
                    } else {
                        return 0;
                    }
                })
                return copy
            }
            if(this.sortBy == "tipster"){
                copy.sort( (a,b) => {
                    if(a.tipster.toLowerCase() < b.tipster.toLowerCase()){
                        return -1;
                    } else if(a.tipster.toLowerCase() > b.tipster.toLowerCase()){
                        return 1;
                    } else {
                        return 0;
                    }
                })
                return copy
            }
            if(this.sortBy == "estimatedTime"){
                copy.sort( (a,b) => {
                    return a - b;
                })
            return copy
            }
            if(this.sortBy == "score"){
                copy.sort( (a,b) => {
                    if(a.score > b.score){
                        return -1;
                    } else if(a.score < b.score){
                        return 1;
                    } else {
                        return 0;
                    }
                })
            return copy
            }

            return copy
        }//slut sortlist







    },//slut computed
    methods:{
        sortByThis(sortThis){
            this.sortBy = sortThis;
            if(sortThis == "activity"){
                this.latestActive = false;
                this.activityActive = true;
                this.categoryActive = false;
                this.tipsterActive = false;
                this.scoreActive = false;
                this.estimatedTimeActive = false;
            } else if(sortThis == "category"){
                this.latestActive = false;
                this.activityActive = false;
                this.categoryActive = true;
                this.tipsterActive = false;
                this.scoreActive = false;
                this.estimatedTimeActive = false;
            } else if(sortThis == "tipster"){
                this.latestActive = false;
                this.activityActive = false;
                this.categoryActive = false;
                this.tipsterActive = true;
                this.scoreActive = false;
                this.estimatedTimeActive = false;
            } else if(sortThis == "estimatedTime"){
                this.latestActive = false;
                this.activityActive = false;
                this.categoryActive = false;
                this.tipsterActive = false;
                this.scoreActive = false;
                this.estimatedTimeActive = true;
            } else if(sortThis == "score"){
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
        emitDelete(key){
            this.$emit('emitDelete', key);
        },
        updateUserScore(){
            this.userScore = event.target.value;
        },
        rateActivity(key){
            this.$emit('rateActivity', {'score':this.userScore, 'key': key});
        }

    },

    props: {
        activityList: Array
    }
} //slut export default
</script>

<style scoped>
    @import url('https://fonts.googleapis.com/css2?family=Quicksand&display=swap');
    *{
        font-family:'Quicksand', sans-serif;
    }
    div.activityCard{
        border-bottom: 2px solid grey;
        margin-bottom: .5rem;
        background-color:#465F6F;
        color:white;
        display: flex;
        justify-content: space-between;

    }
    div.activityCard div:first-child{
        border: 2px solid red;
    }
    div.activityCard div:last-child{
        border: 2px solid grey;
    }
    span{
        font-weight: 600;
    }
    h3{
        padding-top:0.5em;
        padding-bottom:0.3em;
        margin: .3rem .3rem .3rem .5rem

    }
    p{
       margin: .3rem .3rem .3rem .5rem;

    }
    p.created,
    span.created{
        font-size: .7rem;
    }
    .optionDiv{
        display: flex;
        flex-direction: column;
        width: 11rem;
        padding: .2rem 2rem .2rem;
        align-items: center;
        justify-content: space-evenly;

    }
    p.score,
    span.score{
        padding-right: .6rem;
    }
    select{
        margin-top: .3rem;
    }
    .optionDiv button{
        width: 4rem;
        padding: .2rem;
        margin-top: .3rem;
    }
    img.delete{
        object-fit: scale-down;
        height: 3rem;
        padding: .5rem;
        cursor: pointer;
    }
    .sortButtons > button{
        background-color:#96BB53;
        padding:0.5em;
        border:1px solid white;
        /*border-radius:0.5em;*/

    }

    .sortButtons > .activeClass{
        background-color: #EFC748;
    }



</style>