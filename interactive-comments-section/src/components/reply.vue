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


                <p class="you" v-if="currentUser">You</p>
    
                 <p>{{ dataReply.createdAt }}</p>

                 <div class="del-edit" v-if="currentUser">
                    <button class="del" @click="deleteReply">
                        <img src="../archives/images/icon-delete.svg" alt="icondelete">
                        Delete
                    </button>

                    <button class="edit" @click="editReply"> <img src="../archives/images/icon-edit.svg" alt="iconedit">Edit</button>
                </div>

                 <button class="show-input-reply"
                 v-if="!currentUser" @click="toggleReplyInput">
                    <svg width="14" height="13" xmlns="http://www.w3.org/2000/svg"><path d="M.227 4.316 5.04.16a.657.657 0 0 1 1.085.497v2.189c4.392.05 7.875.93 7.875 5.093 0 1.68-1.082 3.344-2.279 4.214-.373.272-.905-.07-.767-.51 1.24-3.964-.588-5.017-4.829-5.078v2.404c0 .566-.664.86-1.085.496L.227 5.31a.657.657 0 0 1 0-.993Z" fill="#5357B6"/>
                    </svg>
                     Reply
                    </button>
            </div>
            <p class="content">{{ dataReply.content }}</p>

            <div class="section-reply" v-if="showReplyInput">
                <textarea name="text" id="5" cols="30" rows="10" v-model="replyText" ></textarea>
                
                <button class="add-replay" @click="addReply">Reply</button>
            </div>

            <div class="section-reply" v-if="editingReply">
                <textarea name="text" id="5" cols="30" rows="4" v-model="replyTextEdit">
                </textarea>
                
                <button class="add-replay" @click="addEditedReply">Edit</button>
            </div>
            
        </div>
    </div>
</template>

<script>
import {generateCommentId} from '../idService';

export default {
    props: ['dataReply', 'parentComment', 'alldata', 'index'],
    data(){
        return{
            amoutScore: this.dataReply.score,
            showReplyInput: false,
            replyText: '@'+this.dataReply.user.username,
            editingReply: false,
            replyTextEdit: ''
        }
    },
    computed:{
        currentUser(){
            return this.dataReply.user.username === this.alldata.currentUser.username
        },
        replyTo(){
            return this.parentComment.user.username
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
                id: generateCommentId(),
                content: this.replyText,
                createdAt: this.currentDate(),
                score: 0,
                replyingTo: '',
                user: {
                    image: { 
                    png: '',
                    webp: ''
                    },
                    username: this.alldata.currentUser.username
                }
            };
            this.parentComment.replies.push(newReply);
            this.replyText = '';
            this.showReplyInput = false;
        },
        currentDate(){
            const currentDate = new Date();

            const day = currentDate.getDate().toString().padStart(2, '0');
            const month = currentDate.toLocaleString('default', {month: 'short'});
            const year = currentDate.getFullYear().toString().slice(-2);

            const formatedDate = `${day}/${month}/${year}`;

            return formatedDate;
        },
        deleteReply(){
            this.parentComment.replies.splice(this.index, 1)
        },
        editReply(){
            this.editingReply = !this.editingReply
        },
        addEditedReply(){
            this.dataReply.content = this.replyTextEdit
            if (this.dataReply.content === ''){
                this.parentComment.replies.splice(this.index, 1)
            }
            this.replyTextEdit = ''
            this.editingReply = false
        },

        
        
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