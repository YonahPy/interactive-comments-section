<template>
    
        
    <section>
        <comments  v-for="comment in data.comments" :key="comment.id" :dataComments="comment">
        </comments>
        
    </section>
    
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
@import url('https://fonts.googleapis.com/css2?family=Rubik:wght@400;600;700&display=swap');
*{
    font-family: 'Rubik', sans-serif;
    margin: 0;
    padding: 0;
}
    section{
        width: 60vw;
        margin: 0 auto;
        margin-top: 40px;
        
    }
    p{
        color: hsl(211, 10%, 45%);
    }
</style>