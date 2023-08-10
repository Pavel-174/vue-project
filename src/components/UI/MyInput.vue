<template>
    <input 
        :value="modelValue" 
        @input="updateInput" 
        class="input" 
        type="text"
    >
  </template>
  
  <script>
  export default {
    name: 'MyInput',
    props: {
      modelValue: [String, Number]
    },
    methods: {
      updateInput(event) {
        this.$emit('update:modelValue', event.target.value)
      }
    }
  }
  </script>

<style scoped>
.input {
    border: 3px solid teal;
    width: 100%;
    padding: 10px 15px;
    margin-top: 15px;
}
</style>