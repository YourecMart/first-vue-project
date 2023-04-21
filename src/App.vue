<template>
    <div class="app">
        <h1>Страница с постами</h1>
        <div class="app__btns">
            <my-button @click="toggleModal">Создать пост</my-button>
            <my-select @change="sortPosts" :options="sortOptions" :value="selectedSort"/>
        </div>
        
        <my-dialog v-model:show="dialogVisible">
            <post-form @create="createPost" />
        </my-dialog>
        <post-list @removePost="removePost" :posts="posts" v-if="!isLoading" />
        <div style="font-weight: 700; font-size: 20px;" v-else>Идет загрузка...</div>

    </div>
</template>

<script>
import PostForm from '@/components/PostForm.vue'
import PostList from '@/components/PostList.vue'
import axios from 'axios'
export default {
    components: {
        PostList,
        PostForm,
    },
    data() {
        return {
            posts: [],
            dialogVisible: false,
            isLoading: false,
            selectedSort: '',
            sortOptions: [
                {value: 'title', name: 'По названию'},
                {value: 'body', name: 'По описанию'}
            ]
        }

    },
    methods: {
        createPost(post) {
            this.posts.push(post)
            this.dialogVisible = false
        },
        removePost(post) {
            console.log(post)
            this.posts = this.posts.filter((currentPost) => currentPost.id !== post.id)
        },
        toggleModal() {
            this.dialogVisible = true
        },
        async fetchPosts() {
            try {
                this.isLoading = true
                setTimeout(async () => {
                    const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10')
                    this.posts = response.data
                    this.isLoading = false
                }, 1000)
            } catch (error) {
                alert('Ошибка', error)
            }
        },

    },
    mounted() {
        console.log('mounted!')
        this.fetchPosts();
    },
  
    computed: {
        sortPosts(){
            console.log(this.selectedSort)
            if (!this.selectedSort) {
                return this.posts
            }
          return this.posts.sort((a, b) => a[this.selectedSort].localCompare(b[this.selectedSort]))
        }
    }

}
</script>


<style >
*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

.app {
    padding: 20px;
    color: teal;
}
.app__btns{
    margin-top: 15px; 
    margin-bottom: 15px;
    display: flex;
    justify-content: space-between;
}
</style>
