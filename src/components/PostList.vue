<template>
    <div>
        <h3>Список постов</h3>
        <PostItem  
          v-for="post in posts"
          :post="post"
        />
    </div>
</template>

<script>
import PostItem from './PostItem.vue';

export default {
    props: {
        posts: {
            type: Array,
            required: true
        }
    },
    components: { PostItem }
}
</script>

<style scoped>
.post {
    padding: 15px;
    border: 3px solid teal;
    margin-top: 15px;
}
</style>