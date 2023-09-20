<template>
    
        
    <comments  v-for="comment in data.comments" :key="comment.id" :dataComments="comment">
    </comments>
        
    
</template>

<script>
    import data from '../archives/data.json'
    import comments from './comments.vue'

    export default{
        components:{
            comments
        },
        data(){
            return{
                data: data
            }
        }
    }

</script>

<style>

</style>