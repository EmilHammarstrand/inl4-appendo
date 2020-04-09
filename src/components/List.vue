<template>
    <div class="root">

        <button>Add activity</button>

        <div class="sortButtons">
            <button @click="sortByThis('activity')">Activity</button>
            <button @click="sortByThis('category')">Category</button>
            <button @click="sortByThis('tipster')">Tipster</button>
            <button @click="sortByThis('estimatedTime')">Time</button>
            <button @click="sortByThis('score')">Score</button>
        </div>
        
        <div v-for="activity in sortList" class="activityCard" :key="activity.activity">
            <h3>{{activity.activity}}</h3> 
            <p> <span>Category:</span>  {{activity.category}}</p>
            <p> <span>Score: </span> {{activity.score}}</p>
            <p> <span>Tipster:</span>  {{activity.tipster}}</p>
            <p> <span>Estimated time:</span>  {{activity.estimatedTime}}</p>
            <p> <span>Published at:</span>  {{activity.date}}</p>
        </div>
        
    </div>
</template>

<script>
export default {
    data: () => ({

        sortBy: "default"

    }),
    computed:{

        sortList(){

            let copy = [...this.activityList];
            
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
                if(a.estimatedTime.toLowerCase() < b.estimatedTime.toLowerCase()){
                    return -1;
                } else if(a.estimatedTime.toLowerCase() > b.estimatedTime.toLowerCase()){
                    return 1;
                } else {
                    return 0;
                }
            })
            return copy
            }
            if(this.sortBy == "score"){
                copy.sort( (a,b) => {
                if(a.score.toLowerCase() < b.score.toLowerCase()){
                    return -1;
                } else if(a.score.toLowerCase() > b.score.toLowerCase()){
                    return 1;
                } else {
                    return 0;
                }
            })
            return copy
            }

            return copy
            
            

           
        },
        
    },//slut computed
    methods:{
        sortByThis(sortThis){
            this.sortBy = sortThis;
        },

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
    .sortButtons > button{
        background-color:#96BB53;
        padding:0.5em;
        border:1px solid white;
        border-radius:0.5em;
       
    }


</style>