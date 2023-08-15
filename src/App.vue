<template>
    <div class="app">
        <h1>Страница с постами</h1>
        <div class="app__buttons">
            <MyButton
              class="button__post"
              @click="openPopup"
            >
            Создать пост
            </MyButton>
            <MySelect 
              v-model="selectedSort" 
              :options="sortOptions"
            >
            </MySelect>
        </div>
        <MyPopup v-model:show="popupOpened">
            <PostForm
                @create="createPost"
            />
        </MyPopup>
        <PostList 
          :posts="posts"
          @remove="removePost"
          v-if="!isPostLoading"
        />
        <div v-else="isPostLoading">Идет загрузка...</div>
    </div>
</template>

<script>
import PostForm from '@/components/PostForm'
import PostList from '@/components/PostList'
import MyPopup from './components/UI/MyPopup.vue';
import MyButton from './components/UI/MyButton.vue';
import axios from 'axios';
import MySelect from './components/UI/MySelect.vue';

export default {
    components: {
    PostForm, 
    PostList,
    MyPopup,
    MyButton,
    MySelect
},
    data () {
        return {
            posts: [],
            popupOpened: false,
            isPostLoading: false,
            selectedSort: '',
            sortOptions: [
                {value: 'title', name:'По названию'},
                {value: 'body', name:'По содержимому'},
            ]
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
                this.isPostLoading = true;
                const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10');
                this.posts = response.data;
            } catch (event) {
                alert("Ошибка!")
            } finally {
                this.isPostLoading = false;
            }
        },
    },
    mounted() {
        this.fetchPosts();
    }
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

.app__buttons{
    display: flex;
    justify-content: space-between;
    margin: 20px 0;
}

.button__post{
    
}
</style>