<template>
    <button class="btn">
        <slot></slot>
    </button>
</template>
<script>
export default {
    name: 'my-button'
}

</script>
<style scoped>
.btn {
    
    padding: 10px 15px;
    background: none;
    color: rgb(0, 128, 13);
    border:  2px solid rgb(0, 128, 13);
    border-radius: 5px;
    margin-right: 10px;
    margin-top: 10px;
}

.btn:hover {
    background-color: rgb(0, 128, 13);
    color: white;

}

</style>