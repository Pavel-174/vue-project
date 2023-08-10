<template>
    <div v-if="posts.length > 0">
        <h3>Список постов</h3>
        <PostItem  
          v-for="post in posts"
          :post="post"
          :key="post.id"
          @remove="$emit('remove', post)"
        />
    </div>
    <h3 
        class="posts__header"
        v-else="posts.length === 0"
    >
        Список постов пуст
    </h3>
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
.posts__header {
    color: red;
}
</style>