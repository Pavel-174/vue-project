<template>
    <div>
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
                ]
            }
        },

        methods: {
        },
    }
    
</script>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

.post {
    padding: 15px;
    border: 3px solid teal;
    margin-top: 15px;
}
</style>