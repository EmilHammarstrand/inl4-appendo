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
            <label for="dropdown">Category: </label>
             <select name="dropdown" v-model="selected">
                <option>Outside</option>
                <option>Food</option>
                <option>Training</option>
                <option>Thinking</option>
             </select>
        </div>
        <div class="form-group">
            <label for="estimatedTime">Estimated time: </label>
            <input name="estimatedTime" type="number" v-model="estimatedTime" min="3" max="15" >
        </div>
        <div class="form-group">
            <button :disabled="!isCompleted || !nameIsValid || !activityIsValid" @click="formResult = true"> Post</button>
        </div>
         
        <span v-if="formResult"> Hello {{name}}, you choose {{activity}} in category {{selected}}, estimated time {{estimatedTime}} minutes {{}}</span>
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
            return new Date().toLocaleString();
        }
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
</style>

