<template>
    <form @submit.prevent >
        <h4>Create new post</h4>

        <my-input 
        v-model = "post.title"
         type="text" placeholder="Title"/>

        <my-input  
        v-model = "post.description"
         type="text" placeholder="Description"/>

        <my-button 
        @click="createPost"
        class="btn_form"
        >Create</my-button >
    </form>
</template>
<script>

export default {
    
    data() {
        return {
            post: {
                title: '',
                description: '',
            }
            
        }
    },
    methods:{
        createPost() {
            this.post.id = new Date().toLocaleString();
            this.$emit('create', this.post)
            this.post = {
                title: '',
                body: ''
            }
        }
    }
}
</script>
<style scoped>
form {
    display: flex;
    flex-direction: column;
}

.btn_form {
    align-self: flex-start;
    margin: 15px;
    margin-left: 0;
}



</style>