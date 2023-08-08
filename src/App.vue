<template>
    <div class="app">
        <form @submit.prevent>
            <h4>Создание поста</h4>
            <input 
                v-bind:value="title"
                @input="inputTitle"
                class="input" 
                type="text" 
                placeholder="Название поста"
            >
            <input 
                v-bind:value="body"
                @input="body = $event.target.value"
                class="input" 
                type="text" 
                placeholder="Описание поста"
            >
            <button 
                class="button" 
                @click="createPost"
            >
            Создать пост
            </button>
        </form>
        <div class='post' v-for="post in posts">
            <div> <strong> Название: </strong> {{ post.title }} </div>
            <div> <strong> Описание: </strong> {{ post.body }} </div>
        </div>
    </div>
</template>

<script>
    export default {
        data () {
            return {
                posts: [
                    { id: 1, title: "JavaScript", body: "JavaScript универсальный язык програмирования" },
                    { id: 2, title: "JavaScript 1", body: "JavaScript универсальный язык програмирования 1" },
                    { id: 3, title: "JavaScript 2", body: "JavaScript универсальный язык програмирования 2" },
                ],
                title: '',
                body: ''
            }
        },

        methods: {
            createPost() {
                const newPost = {
                    id: Date.now(),
                    title: this.title,
                    body: this.body,
                }
                this.posts.push(newPost);
            },

            inputTitle (event) {
                this.title = event.target.value;
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

.post {
    padding: 15px;
    border: 3px solid teal;
    margin-top: 15px;
}

form {
    display: flex;
    flex-direction: column;
}

.input {
    border: 3px solid teal;
    width: 100%;
    padding: 10px 15px;
    margin-top: 15px;
}

.button{
    align-self: center;
    margin-top: 15px;
    padding: 10px 15px;
    background: none;
    color: teal;
    border: 2px solid teal;
}

</style>