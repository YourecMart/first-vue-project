<template>
     <div v-if="posts.length >= 1" class="posts-container" >
        <h3>Список постов</h3>
        <post-item @removePost="$emit('removePost', post)" :key="post.id + index" :post="post"  v-for="(post,index) in posts"/>
     </div>
    
     <h2 style="color:teal; text-align:center" v-else>
        Список пуст
     </h2>

     
    
</template>

<script>
import PostItem from './PostItem.vue';
    export default {
        components: {
            PostItem,
        },
        props: {
            posts: {
                type: Array,
                required: true,
            }
        },
        methods: {
          
        }
    }
</script>

<style scoped>
.posts-container {
    display: flex;
    flex-direction: column;
    gap: 1rem;
    margin: 0 auto;
}



</style>