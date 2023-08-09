<template>
    <div class="app">
        <PostForm
          @create="createPost"
        />
        <PostList 
          :posts="posts"
        />
    </div>
</template>

<script>
import PostForm from '@/components/PostForm'
import PostList from '@/components/PostList'

export default {
    components: {
        PostForm, PostList
    },
    data () {
        return {
            posts: [
                { id: 1, title: "JavaScript", body: "JavaScript универсальный язык програмирования" },
                { id: 2, title: "JavaScript 1", body: "JavaScript универсальный язык програмирования 1" },
                { id: 3, title: "JavaScript 2", body: "JavaScript универсальный язык програмирования 2" },
            ]
        }
    },
    methods: {
        createPost(post) {
            this.posts.push(post);
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
</style>