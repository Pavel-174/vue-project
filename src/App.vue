<template>
    <div> Hello world! </div>
    <div> Лайки: <strong> {{ likes }} </strong> </div>
    <div> Дизлайки: <strong> {{ dislikes }} </strong> </div>
    <div>
        <button v-on:click="addLike">Like</button>
        <button v-on:click="addDislike">Dislike</button>
    </div>
</template>

<script>
    export default {
        data () {
            return {
                likes: 0,
                dislikes: 0,
            }
        },

        methods: {
            addLike (){
                this.likes += 1;
            },
            addDislike (){
                this.dislikes += 1;
            }
        },
    }
    
</script>

<style></style>