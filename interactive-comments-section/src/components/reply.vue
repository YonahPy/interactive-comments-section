<template>
    <div class="comments comments-reply">
        
        <div class="buttons">
            <button class="increase" @click="increaseLike">+</button>
            <span>{{ amoutScore }}</span>
            <button class="decrease" @click="decreaseLike">-</button>
        </div>
        <div class="line">
            <div class="profile">
                 <img v-bind:src="dataReply.user.image.png" alt="perfil">
                 <p class="username">{{ dataReply.user.username }}</p>
                 <p>{{ dataReply.createdAt }}</p>
                 <button class="show-input-reply" @click="toggleReplyInput">
                    <svg width="14" height="13" xmlns="http://www.w3.org/2000/svg"><path d="M.227 4.316 5.04.16a.657.657 0 0 1 1.085.497v2.189c4.392.05 7.875.93 7.875 5.093 0 1.68-1.082 3.344-2.279 4.214-.373.272-.905-.07-.767-.51 1.24-3.964-.588-5.017-4.829-5.078v2.404c0 .566-.664.86-1.085.496L.227 5.31a.657.657 0 0 1 0-.993Z" fill="#5357B6"/>
                    </svg>
                     Reply
                    </button>
            </div>
            <p class="content">{{ dataReply.content }}</p>

            <div class="section-reply" v-if="showReplyInput">
                <input type="text" v-model="replyText">
                <button class="add-replay" @click="addReply">Reply</button>
            </div>
            
        </div>
    </div>
</template>

<script>
export default {
    props: ['dataReply', 'parentComment'],
    data(){
        return{
            amoutScore: this.dataReply.score,
            showReplyInput: false,
            replyText: '',
            generateId: 6,
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
            this.parentComment.replies.push(newReply);
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
    .line{
        width: 100%;
    }
    .comments-reply .buttons{
        width: 35px;
    }
</style>