<template>
    <div class="root">
        <div class="form-group">
            <label for="name">Name: </label>
            <input type="text" name="name" placeholder="Enter your name" v-model="name" :class="nameClass" @blur.once="nameIsTouched = true" >
            <span v-if="nameIsTouched && !nameIsValid" class="error"> {{ nameErrorMessage }} </span>
        </div>
        <div class="form-group">
            <label for="activity">Activity suggestion: </label>
            <input type="text" placeholder="Enter a short suggestion" name="activity" v-model="activity" :class="activityClass" @blur.once="activityIsTouched = true" >
            <span v-if="!activityIsValid && activityIsTouched" class="error"> {{ activityErrorMessage }} </span>
        </div>
        <div class="form-group">
             <select v-model="selected">
                <option>Outside</option>
                <option>Food</option>
                <option>Training</option>
                <option>Thinking</option>
             </select>
         </div>
        <div class="form-group">
            <button @click="postActivityBtn"> Post</button>
        </div>
         
        <span> {{name}} {{activity}} {{selected}}</span>
    </div>
</template>

<script>
export default {
    data: () => ({
        name: "",
        activity: "",
        nameIsTouched: false,
        activityIsTouched: false
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
        activityErrorMessage(){
            return "Max characters is 10"
        },
        activityIsValid() {
            return this.activity.length <= 10;
        },
        activityClass() {
			if( !this.activityIsTouched ) return '';
			return this.activityIsValid ? 'valid' : 'invalid';
        }
    },

    methods: {
        postActivityBtn(){
            this.name;
            this.activity;
        }
    }



}

</script>

<style scoped>
    input.valid { border-color: green; }
    input.invalid { border-color: red; }

    textarea.valid { border-color: green; }
    textarea.invalid { border-color: red; }
</style>

