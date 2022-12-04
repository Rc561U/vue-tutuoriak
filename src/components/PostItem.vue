<template>
    <div class="post">
        <div>
            <div><strong>ID:</strong> {{ post.id}}</div>    
        <div><strong>Name:</strong> {{ post.title}}</div>    
        <div><strong>Description: </strong>{{ post.body }}</div>   
        </div>
        <div class="post__btns">
            <!-- <button>Edit</button> -->
            <my-button
                @click="showDialog" style="margin: 20px;"
                >Delete
            </my-button>
            <my-dialog  v-model:show="dialogVisible" >
                <h1> Are you sure?</h1>
                <div class="btn_action">
                    <my-button class="delete_btn"
                    @click="closeDialog"
                    >Disagree</my-button>
                    <my-button
                    @click.stop="deletePost"
                    >Agree</my-button>
                </div>
                
            </my-dialog>
            
            
        </div>
    </div>
</template>
<script>
import  MyDialog from "@/components/UI/MyDialog";
import  MyButton from "@/components/UI/MyButton";
export default {

    props: {
        post: {
            type: Object,
            required: true,
        }
    },
    data() {
        return {
            dialogVisible: false,
        }
    },
    components: { MyDialog },
    methods:{
        showDialog() {
            this.dialogVisible = true;
        },
        closeDialog() {
            this.dialogVisible = false;
        },
        deletePost() {
            this.dialogVisible = false;
            this.$emit('remove', this.post);
        }
    },
}

</script>
<style scoped>
.post {
    padding: 15px;
    border: 5px solid rgb(0, 128, 13);
    border-radius: 5px;
    margin-top: 15px;
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.delete_btn {
/*    margin: 10px;*/
}

.btn_action {
    text-align: center;
}
</style>