<template>
    <div class="app">
        <h1>Страница с постами</h1>
        <MyButton
            class="button__post"
            @click="fetchPosts"
        >
            Получить посты
        </MyButton>
        <MyButton
            class="button__post"
            @click="openPopup"
        >
            Создать пост
        </MyButton>
        <MyPopup v-model:show="popupOpened">
            <PostForm
                @create="createPost"
            />
        </MyPopup>
        <PostList 
          :posts="posts"
          @remove="removePost"
        />
    </div>
</template>

<script>
import PostForm from '@/components/PostForm'
import PostList from '@/components/PostList'
import MyPopup from './components/UI/MyPopup.vue';
import MyButton from './components/UI/MyButton.vue';
import axios from 'axios';

export default {
    components: {
    PostForm, PostList,
    MyPopup,
    MyButton
},
    data () {
        return {
            posts: [],
            popupOpened: false
        }
    },
    methods: {
        createPost(post) {
            this.posts.push(post);
            this.popupOpened = false;
        },
        removePost(post) {
            this.posts = this.posts.filter(p => p.id !== post.id)
        },
        openPopup() {
            this.popupOpened = true;
        },

        async fetchPosts() {
            try {
                const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10');
                this.posts = response.data;
                console.log(response)
            } catch (event) {
                alert("Ошибка!")
            }
        },
    },
}
</script>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

.app {
    padding: 20px;
}
.button__post{
    margin: 20px 0;
}
</style>