<template>
    <div class="comment-field">
        <img src="#" alt="perfil">

        <textarea name="text" id="6" cols="30" rows="4" placeholder="Add a comment..." v-model="commentText"></textarea>

        <button class="send" @click="addComment">Send</button>
    </div>
</template>

<script>
import {generateCommentId} from '../idService';
    export default{
        props: ['dataComment'],
        data(){
            return{
                commentText: '',

            }
        },
        methods:{
            
            addComment(){
                const newComment = {
                    id: generateCommentId(),
                    content: this.commentText,
                    createdAt: this.currentDate(),
                    score: 0,
                    replyingTo: '',
                    user: {
                        image: { 
                        png: '',
                        webp: ''
                        },
                        username: this.dataComment.currentUser.username
                    },
                    replies: []
                };
            
            this.dataComment.comments.push(newComment);
            this.commentText = ''

            },

            currentDate(){
            const currentDate = new Date();

            const day = currentDate.getDate().toString().padStart(2, '0');
            const month = currentDate.toLocaleString('default', {month: 'short'});
            const year = currentDate.getFullYear().toString().slice(-2);

            const formatedDate = `${day}/${month}/${year}`;

            return formatedDate;
        }
    }
}
</script>

<style scoped>
    .comment-field{
        display: flex;
        padding: 20px;
        border-radius: 10px;
        background-color:  hsl(0, 0%, 100%);
        box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.185);
    }
    textarea{
        margin-left: 30px;
        border-radius:10px ;
        width: 80%;
        height: 50px;
        padding: 20px;
        border: 1px solid black;
        font-size: 16px;
    }
    textarea:focus{
        border: 1px solid hsl(238, 40%, 52%);
        outline: none;
    }
    .send{
        width: 100px;
        height: 50px;
        margin-left: 15px;
        background-color: hsl(238, 40%, 52%);
        color: white;
        font-weight: bold;
        font-size: 17px;
        border: none;
        border-radius: 10px;
    }
    .send:hover{
        background-color: hsla(238, 40%, 52%, 0.548);
    }
</style>