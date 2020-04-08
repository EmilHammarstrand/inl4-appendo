<template>
    <div class="root">
        <div class="form-group">
            <label for="name">Tipser: </label> <br />
            <input type="text" name="name" placeholder="Enter your name" v-model="name" :class="nameClass" @blur.once="nameIsTouched = true" >
            <span v-if="nameIsTouched && !nameIsValid" class="error"> {{ nameErrorMessage }} </span>
        </div>
        <div class="form-group">
            <label for="activity">Activity: </label> <br />
            <input type="text" placeholder="Enter a short suggestion" name="activity" v-model="activity" :class="activityClass" @blur.once="activityIsTouched = true" >
            <span v-if="!activityIsValid && activityIsTouched" class="error"> {{ activityErrorMessage }} </span>
        </div>
        <div class="form-group">
            <label for="dropdown">Category: </label> <br />
             <select name="dropdown" v-model="selected" :class="categoryClass" @blur.once="categoryIsTouched = true">
                <option>Outside</option>
                <option>Food</option>
                <option>Training</option>
                <option>Thinking</option>
             </select>
             <span v-if="categoryIsValid && categoryIsTouched" class="error"> {{ categoryErrorMessage }} </span>
        </div>
        <div class="form-group">
            <label for="estimatedTime">Estimated minutes: </label> <br />
            <input class="estTime" name="estimatedTime" type="number" v-model="estimatedTime" min="3" max="15" :class="timeClass" @blur.once="timeIsTouched = true" >
            <span v-if="!timeIsValid && timeIsTouched" class="error"> {{ timeErrorMessage }} </span>
        </div>
        <div class="form-group">
            <button :disabled="!isCompleted || !nameIsValid || !activityIsValid" @click="formResult = true;"> Post</button>
        </div>
         
        <span v-if="formResult"> Hello {{name}}, you choose {{activity}} in category {{selected}}, estimated time {{estimatedTime}} minutes, published: {{todaysDate}} </span>
    </div>
</template>

<script>
export default {
    data: () => ({
        name: "",
        activity: "",
        selected: "",
        estimatedTime: "",
        date: "",
        nameIsTouched: false,
        activityIsTouched: false,
        categoryIsTouched: false,
        timeIsTouched: false,
        formResult: false
    }),

    computed: {
        nameErrorMessage(){
            return "Please enter at least two characters."
        },
        nameIsValid() {
            return this.name.length >= 2;
        },
        nameClass() {
			if( !this.nameIsTouched ) return '';
			return this.nameIsValid ? 'valid' : 'invalid';
        },
        categoryIsValid() {
            return this.selected == 0;
        },
        categoryClass() {
			if( !this.categoryIsTouched ) return '';
			return this.categoryIsValid ? 'valid' : 'invalid';
        },
        activityErrorMessage(){
            return "Must be between 2-10 characters"
        },
        activityIsValid() {
            let asd = this.activity.length <= 10 && this.activity.length >= 2;
            return asd;
        },
        activityClass() {
			if( !this.activityIsTouched ) return '';
			return this.activityIsValid ? 'valid' : 'invalid';
        },
        isCompleted(){
            return this.name && this.activity && this.selected && this.estimatedTime;
        },
        todaysDate(){
         let todaysDate = new Date().toLocaleString();
         return todaysDate;
        },
        categoryErrorMessage(){
            return "You must choose a category";
        },
        timeErrorMessage(){
            return "Must be between 3-15 minutes";
        },
        timeIsValid() {
            let qwe = this.estimatedTime >=3 && this.estimatedTime <= 15;
            return qwe;
        },
        timeClass() {
			if( !this.timeIsTouched ) return '';
			return this.timeIsValid ? 'valid' : 'invalid';
        },
    },

    methods: {
        postActivityBtn(){
            
        }
    }



}

</script>

<style scoped>
    input.valid { border-color: green; }
    input.invalid { border-color: red; }

    textarea.valid { border-color: green; }
    textarea.invalid { border-color: red; }

    select.valid { border-color: red; }
    select.invalid { border-color: green; }

    .error{
        color: red;
    }
    .form-group{
        margin: 1em;

    }
    .estTime{
        width: 2.3em;
    }
</style>

