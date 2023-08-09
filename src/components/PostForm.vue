<template>
    <form @submit.prevent>
        <h4>Создание поста</h4>
        <input 
            v-model="post.title"
            class="input" 
            type="text" 
            placeholder="Название поста"
        >
        <input 
            v-model="post.body"
            class="input" 
            type="text" 
            placeholder="Описание поста"
        >
        <Button
            class="button button__form" 
            @click="createPost"
        >
        Создать пост
        </Button>
    </form>
</template>

<script>
export default {
    data() {
        return {
            post: {
                title: '',
                body: ''
            }
        }
    },
    methods: {
        createPost() {
            const newPost = {
                id: Date.now(),
                title: this.title,
                body: this.body,
            }
            this.$emit('create', this.post)
            this.post = {
                title: '',
                body: ''
            }
        },
    },
}
</script>

<style scoped>
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

.button__form {
    align-self: center;
    margin-top: 15px;
}
</style>