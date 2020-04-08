<template>
    <div class="root">
        <button @click="sortByThis('activity')">Activity</button>
        <button @click="sortByThis('category')">Category</button>
        <button @click="sortByThis('tipster')">Tipster</button>
        <button @click="sortByThis('estimatedTime')">Time</button>
        <button @click="sortByThis('score')">Score</button>
        <div v-for="activity in sortList" class="activityCard" :key="activity.activity">
            <h3>{{activity.activity}}</h3> 
            <p> <span>Category:</span>  {{activity.category}}</p>
            <p> <span>Score: </span> {{activity.score}}</p>
            <p> <span>Tipster:</span>  {{activity.tipster}}</p>
            <p> <span>Estimated time:</span>  {{activity.estimatedTime}}</p>
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
    div.activityCard{
        border: 2px solid grey;
        margin-bottom: .5rem;

    }
    span{
        font-weight: 600;
    }
    p,
    h3{
        margin-left: .5rem;
    }


</style>