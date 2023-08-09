<template>
    <div class='post'>
        <div>
            <div> <strong> Название: </strong> {{ post.title }} </div>
            <div> <strong> Описание: </strong> {{ post.body }} </div>
        </div>
        <div class="post__buttons">
            <Button>Удалить</Button>
        </div>
    </div>
</template>

<script>
import Button from '@/components/UI/Button.vue'

export default {
    components: {
        Button
    },
    props: {
        post: {
            type: Object,
            required: true
        }
    }
}
</script>

<style>
.post {
    padding: 15px;
    border: 3px solid teal;
    margin-top: 15px;
    display: flex;
    align-items: center;
    justify-content: space-between;
}
</style>