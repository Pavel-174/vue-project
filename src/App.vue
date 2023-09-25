<template>
    <div class="app">
        <h1>Страница с постами</h1>
        <MyInput
          v-model="searchQuery"
          placeholder="Поиск..."
        >
        </MyInput>
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
          :posts="sortedAndSearchedPosts"
          @remove="removePost"
          v-if="!isPostLoading"
        />
        <div v-else="isPostLoading">Идет загрузка...</div>
        <div class="page__wrapper">
            <div 
              v-for="pageNumber in totalPages"
              :key="pageNumber"
              class="page"
              :class="{
                'current-page': page === pageNumber
              }"
              @click="changePage(pageNumber)"
            >{{ pageNumber }}</div>
        </div>
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
            searchQuery: '',
            page: 1,
            limit: 10,
            totalPages: 0,
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
        changePage(pageNumber) {
            this.page = pageNumber;
        },
        async fetchPosts() {
            try {
                this.isPostLoading = true;
                const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
                    params: {
                        _page: this.page,
                        _limit: this.limit
                    }
                });
                this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit)
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
    },
    computed: {
        sortedPosts() {
            return [...this.posts].sort( (post1, post2) => post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]) )
        },
        sortedAndSearchedPosts() {
            return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
        }
    },
    watch: {
        page() {
            this.fetchPosts()
        }
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

.page__wrapper{
    display: flex;
    margin-top: 15px;
}

.page{
    border: 1px solid black;
    padding: 10px;
}

.current-page{
    border: 2px solid teal;
}
</style>