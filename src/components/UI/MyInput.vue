<template lang="">
    <input v-bind:value="modelValue" @input="updateInput" class="input" type="text">
</template>
<script>
export default {
    name: 'my-input',
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
    width: 100%;
    border: 1px solid rgb(0, 128, 13);
    border-radius: 5px;
    padding: 10px;
    margin-top: 10px;
}
</style>