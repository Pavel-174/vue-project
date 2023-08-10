<template>
    <form @submit.prevent>
        <h4>Создание поста</h4>
        <MyInput 
            v-model="post.title"
            type="text" 
            placeholder="Название поста"
        />
        <MyInput 
            v-model="post.body"
            type="text" 
            placeholder="Описание поста"
        />
        <MyButton
            class="button button__form" 
            @click="createPost"
        >
        Создать пост
        </MyButton>
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

.button__form {
    align-self: center;
    margin-top: 15px;
}
</style>