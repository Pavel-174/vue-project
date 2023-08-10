<template>
    <div 
        class="popup" 
        v-if="show" 
        @click="closePopup"
    >
        <div 
            @click.stop 
            class="popup__content"
        >
            <slot></slot>
        </div>
    </div>
</template>

<script>
export default {
    name: 'MyPopup',
    props: {
        show: {
            type: Boolean,
            default: false
        }
    },
    methods: {
        closePopup() {
            this.$emit('update:show', false)
        }
    }
}
</script>

<style scoped>
.popup {
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
    background: rgba(0, 0, 0, 0.6);
    position: fixed;
    display: flex;
}

.popup__content{
    margin: auto;
    background-color: white;
    border-radius: 10px;
    min-height: 60px;
    min-width: 290px;
    padding: 30px;
}
</style>