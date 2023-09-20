<template>
    <div>
        
        <div>
            <button>+</button>
            <button>-</button>
        </div>
        <div>
            <div>
                 <img :src="dataComments.user.image.png" alt="perfil">
                 <p>{{ dataComments.user.username }}</p>
                 <p>{{ dataComments.createdAt }}</p>
                 <button>Reply</button>
            </div>
            <p>{{ dataComments.content }}</p>
        </div>
    </div>
</template>

<script>
 export default{
    props: ['dataComments']
 }
</script>

<style>

</style>