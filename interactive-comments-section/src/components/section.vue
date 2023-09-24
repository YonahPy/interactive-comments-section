<template>
    
        
    <section>
        <comments  v-for="comment in data.comments" :key="comment.id" :dataComments="comment">
        </comments>
        
        <commentField :dataComment="data">

        </commentField>
    </section>
    
</template>

<script>
    import data from '../archives/data.json'
    import comments from './comments.vue'
    import commentField from './commentField.vue'

    export default{
        components:{
            comments,
            commentField,
            
        },
        data(){
            return{
                data: data,
                text: ''
            }
        },
        methods:{
            addComment(textComment){
                this.text = textComment;
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
body{
    background-color: hsl(223, 19%, 93%);
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