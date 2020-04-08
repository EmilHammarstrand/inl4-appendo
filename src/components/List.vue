<template>
    <div class="root">
        <div v-for="activity in activityList" class="activityCard" :key="activity.activity">
            <p> {{activity.activity}}</p>
            <p> <span>Category:</span>  {{activity.category}}</p>
            <p> <span>Score: </span> {{activity.score}}</p>
            <p> <span>Source:</span>  {{activity.source}}</p>
        </div>
        
    </div>
</template>

<script>
export default {
    data: () => ({

    }),
    props: {
        activityList: Array
    }
    
}
</script>

<style scoped>
    div.activityCard{
        border: 2px solid grey;
        margin-bottom: .5rem;

    }
    span{
        font-weight: 600;
    }
    p{
        margin-left: .5rem;
    }


</style>