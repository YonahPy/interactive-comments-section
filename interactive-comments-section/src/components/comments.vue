<template>
    <div class="comments">
        
        <div class="buttons">
            <button class="increase">+</button>
            <span>{{ 85 }}</span>
            <button class="decrease">-</button>
        </div>
        <div>
            <div class="profile">
                 <img v-bind:src="dataComments.user.image.png" alt="perfil">
                 <p class="username">{{ dataComments.user.username }}</p>
                 <p>{{ dataComments.createdAt }}</p>
                 <button class="reply">
                    <svg width="14" height="13" xmlns="http://www.w3.org/2000/svg"><path d="M.227 4.316 5.04.16a.657.657 0 0 1 1.085.497v2.189c4.392.05 7.875.93 7.875 5.093 0 1.68-1.082 3.344-2.279 4.214-.373.272-.905-.07-.767-.51 1.24-3.964-.588-5.017-4.829-5.078v2.404c0 .566-.664.86-1.085.496L.227 5.31a.657.657 0 0 1 0-.993Z" fill="#5357B6"/>
                    </svg>
                     Reply
                    </button>
            </div>
            <p class="content">{{ dataComments.content }}</p>
        </div>
    </div>
</template>

<script>
 export default{
    props: ['dataComments']
 }
</script>

<style>
    .comments{
        display: flex;
        margin-bottom: 20px;
        padding: 30px 25px;
        box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.185);
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
    .reply{
        position: absolute;
        right: 0;
        height: 30px;
        border: none;
        font-size: 17px;
        background-color: transparent;
        color: hsl(238, 40%, 52%);
        cursor: pointer;
    }
    .reply img{
        margin-right: 10px;
    }
    .reply:hover{
        color:hsla(238, 40%, 52%, 0.678);
    }
    .reply path:hover{
        fill:hsla(238, 40%, 52%, 0.678);
    }
    .content{
        margin-left: 30px;
    }

    

</style>