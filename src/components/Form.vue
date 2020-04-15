<template>
    <div class="root rootTwo">

        <span v-if="showSuccessMessage" class="successMessage" >{{successMessage}}</span>

        <div class="form-group">
            <label for="activity"> Activity:</label> <br />
            <input type="text" placeholder="A short suggestion..." name="activity" v-model="activity" :class="activityClass" @click="activityIsTouched = true" >
            <span v-if="!activityIsValid && activityIsTouched" class="error"> {{ activityErrorMessage }} </span>
        </div>

        <div class="form-group">
            <label for="name"> Tipster: <span id="opt">(opt.)</span></label> <br />
            <input type="text" name="name" placeholder="Enter your name..." v-model="name">
        </div>

        <div class="form-group">
            <label for="dropdown"> Category:</label> <br />
             <select name="dropdown" class="categoryButton" v-model="selected" :class="categoryClass" @click="categoryIsTouched = true">
                <option>Relax</option>
                <option>Food</option>
                <option>Exercise</option>
                <option>Thinking</option>
             </select>
             <span v-if="categoryIsValid && categoryIsTouched" class="error"> {{ categoryErrorMessage }} </span>
        </div>

        <div class="form-group">
            <label for="estimatedTime"> Estimated minutes:</label> <br />
            <input class="estTime" name="estimatedTime" type="number" v-model="estimatedTime" min="3" max="15" :class="timeClass" @click="timeIsTouched = true" >
            <span v-if="!timeIsValid && timeIsTouched" class="error"> {{ timeErrorMessage }} </span>
        </div>

        <div class="form-group">
            <button class = "btn btn-warning btn-md" :disabled="!isCompleted || !activityIsValid || categoryIsValid || !timeIsValid" @click="findDuplicate(activity);">Post</button>
            <span v-if="duplicate" class="error"> {{ duplicateErrorMessage }} </span>
        </div>
    </div>
</template>

<script>

import Vue from 'vue'
import { BootstrapVue, IconsPlugin } from 'bootstrap-vue'

Vue.use(BootstrapVue)
Vue.use(IconsPlugin)

export default {
    data: () => ({
        name: "",
        activity: "",
        selected: "",
        estimatedTime: "",
        activityIsTouched: false,
        categoryIsTouched: false,
        timeIsTouched: false,
        duplicate: false,
        showSuccessMessage: false
    }),

    props: {
        activityList: Array
    },

    computed: {

        successMessage(){
            return "Your activity was posted successfully."
        },
        duplicateErrorMessage(){
            return "You cant post duplicates, try writing another activity."
        },
        categoryIsValid() {
            return this.selected == 0;
        },
        categoryClass() {
			if( !this.categoryIsTouched ) return '';
			return this.categoryIsValid ? 'valid' : 'invalid';
        },
        activityErrorMessage(){
            return "Must be between 2-20 characters."
        },
        activityIsValid() {
            let activitylength = this.activity.length <= 20 && this.activity.length >= 2;
            return activitylength;
        },
        activityClass() {
			if( !this.activityIsTouched ) return '';
			return this.activityIsValid ? 'valid' : 'invalid';
        },
        isCompleted(){
            return this.activity && this.selected && this.estimatedTime;
        },
        todaysDate(){
         let todaysDate = new Date().toLocaleString();
         return todaysDate;
        },
        categoryErrorMessage(){
            return "You must choose a category.";
        },
        timeErrorMessage(){
            return "Must be between 3-15 minutes.";
        },
        timeIsValid() {
            let estTime1 = this.estimatedTime >=3 && this.estimatedTime <= 15;
            return estTime1;
        },
        timeClass() {
			if( !this.timeIsTouched ) return '';
			return this.timeIsValid ? 'valid' : 'invalid';
        }
    },

    methods: {

        postActivityBtn(){

            if(this.name == ""){
            this.activityList.push({
                activity: this.activity,
                category: this.selected,
                score: "3",
                tipster: "Anonym",
                estimatedTime: this.estimatedTime,
                date: this.todaysDate
            })} else{
                 this.activityList.push({
                activity: this.activity,
                category: this.selected,
                score: "3",
                tipster: this.name,
                estimatedTime: this.estimatedTime,
                date: this.todaysDate
            })}

            this.name = "";
            this.selected = 0;
            this.activity = "";
            this.estimatedTime = "";
            this.activityIsTouched = false;
            this.categoryIsTouched = false;
            this.timeIsTouched = false;

            this.showSuccessMessage = true;
        },

        findDuplicate(activity){
            if(this.activityList.some(value => value.activity == activity)){
                this.duplicate = true;
                this.duplicateErrorMessage;
            }else {
                this.duplicate = false;
                this.postActivityBtn();
            }
        }
    }
};

</script>

<style>
    input.valid { border-color: green; }
    input.invalid { border-color: red; }

    select.valid { border-color: red; }
    select.invalid { border-color: green; }

    .error{
        color: #ff0000db;
        display: inline-block;
        font-weight: 600;
        font-size: 18px;
        position: absolute;
        margin-left: 10px;
    }

    .form-group{
        margin: 1em;
    }
    .estTime{
        width: 186px;

    }
    label, input, button, option{
        font-family: Quicksand;
    }
    label{
        color:white;
    }
    input{
        color: black;
        padding: 5px;
        border: 1px solid #cccccc;
        border-radius: 4px;
        resize: vertical;
    }

    .categoryButton {
        width: 186px;
        padding: 5px;
        border: 1px solid #cccccc;
        border-radius: 4px;
        resize: vertical;
    }

    #opt {
        opacity: 80%;
        font-size: 75%;
    }

    .successMessage{
        color: chartreuse;
        font-size: 20px;
        font-weight: 600;

    }

    .rootTwo div {
        position: relative
    }

</style>