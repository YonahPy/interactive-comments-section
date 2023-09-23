<template>
    <div class="comments">
        
        <div class="buttons">
            <button class="increase" @click="increaseLike">+</button>
            <span>{{ amoutScore }}</span>
            <button class="decrease" @click="decreaseLike">-</button>
        </div>
        <div>
            <div class="profile">
                 <img v-bind:src="dataComments.user.image.png" alt="perfil">
                 <p class="username">{{ dataComments.user.username }}</p>
                 <p>{{ dataComments.createdAt }}</p>
                 <button class="show-input-reply" @click="toggleReplyInput">
                    <svg width="14" height="13" xmlns="http://www.w3.org/2000/svg"><path d="M.227 4.316 5.04.16a.657.657 0 0 1 1.085.497v2.189c4.392.05 7.875.93 7.875 5.093 0 1.68-1.082 3.344-2.279 4.214-.373.272-.905-.07-.767-.51 1.24-3.964-.588-5.017-4.829-5.078v2.404c0 .566-.664.86-1.085.496L.227 5.31a.657.657 0 0 1 0-.993Z" fill="#5357B6"/>
                    </svg>
                     Reply
                    </button>
            </div>
            <p class="content">{{ dataComments.content }}</p>


            <div class="section-reply" v-if="showReplyInput">
                <input type="text" v-model="replyText">
                <button class="add-replay" @click="addReply">Reply</button>
            </div>
            
            <reply v-for="reply in dataComments.replies" :key="reply.id">

            </reply>

            
    </div>
</div>
</template>

<script>

import reply from './reply.vue'

 export default{
    props: ['dataComments'],
    components:{
        reply
    },
    data(){
        return{
            amoutScore: this.dataComments.score,
            showReplyInput: false,
            replyText: '',
            generateId: 4,
        }
    },
    methods:{
        increaseLike(){
            this.amoutScore++;
        },
        decreaseLike(){
            this.amoutScore--;
        },
        toggleReplyInput(){
            this.showReplyInput = !this.showReplyInput
        },
        addReply(){
            const newReply = {
                id: this.generateUniqueId(),
                content: this.replyText,
                createdAt: this.currentDate(),
                score: 0,
                replyingTo: '',
                user: {
                    image: { 
                    png: '',
                    webp: ''
                    },
                    username: "Jonas Santos"
                }
            };
            this.dataComments.replies.push(newReply);
            this.replyText = '';
            this.showReplyInput = false;
        },
        generateUniqueId(){
            this.generateId =  this.generateId + 1;
            return this.generateId;
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

<style>

    .comments{
        display: flex;
        margin-bottom: 20px;
        padding: 30px 25px;
        box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.185);
        background-color:  hsl(0, 0%, 100%);
    }
    .buttons{
        background-color: rgb(226, 222, 222);
        height: 70px;
        border-radius: 15px;
        overflow: hidden;
        width: 60px;
        font-size: 14px;
        color: hsl(238, 40%, 52%);
        display: flex;
        flex-direction: column;
        align-items: center;
        
    }
    .buttons button{
        width: 100%;
        height: 35%;
        border: none;
        background-color: rgba(226, 222, 222, 0.548);
        color: hsl(211, 10%, 45%);
        font-weight: bold;
        font-size: 16px;
        cursor: pointer;
    }
    .profile{
        display: flex;
        margin-bottom: 15px;
        margin-left: 30px;
        position: relative;
        margin-bottom: 30px;
    }
    .username{
        margin-inline: 20px;
        color: black;
    }
    .show-input-reply{
        position: absolute;
        right: 0;
        height: 30px;
        border: none;
        font-size: 17px;
        background-color: transparent;
        color: hsl(238, 40%, 52%);
        cursor: pointer;
    }
    .show-input-reply img{
        margin-right: 10px;
    }
    .show-input-reply:hover{
        color:hsla(238, 40%, 52%, 0.678);
    }
    .show-input-reply path:hover{
        fill:hsla(238, 40%, 52%, 0.678);
    }
    .content{
        margin-left: 30px;
        margin-bottom: 20px;
        
    }
    .section-reply{
        display: flex;
        
    }
    .section-reply input{
        margin-left: 30px;
        border-radius:10px ;
        width: 80%;
        height: 100px;
        border: 1px solid black;
        
    }
    .section-reply input:focus{
        border: 1px solid hsl(238, 40%, 52%);
        outline: none;
    }
    .add-replay{
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
    .add-replay:hover{
       background-color: hsla(238, 40%, 52%, 0.548);
    }
    .comments .comments-reply .buttons{
        width: 35px;
        
    }
.teste{
    width: 100%
}

    

</style>