<template>
    <div v-if="posts.length > 0">
        <h3>Список постов</h3>
        <transition-group name="post-list">
            <PostItem  
              v-for="post in posts"
              :post="post"
              :key="post.id"
              @remove="$emit('remove', post)"
            />
        </transition-group>
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
.post-list-item {
  display: inline-block;
  margin-right: 10px;
}
.post-list-enter-active,
.post-list-leave-active {
  transition: all 1s ease;
}
.post-list-enter-from,
.post-list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}

.post-list-move {
  transition: transform 0.8s ease;
}
</style>