<template>
    <div class="app">
        <h1>Страница с постами</h1>
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

export default {
    components: {
    PostForm, PostList,
    MyPopup,
    MyButton
},
    data () {
        return {
            posts: [
                { id: 1, title: "JavaScript", body: "JavaScript универсальный язык програмирования" },
                { id: 2, title: "JavaScript 1", body: "JavaScript универсальный язык програмирования 1" },
                { id: 3, title: "JavaScript 2", body: "JavaScript универсальный язык програмирования 2" },
            ],
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
        }
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
    margin: 20px 0gi;
}
</style>