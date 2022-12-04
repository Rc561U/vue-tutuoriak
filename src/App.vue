<template>
<div class="app">
    <h1>Post page absolutely vue </h1>
    <div class="app_btns">
        <my-button
        class="btn_form_dialog"
        @click="showDialog" 
        >Create post
        </my-button>

        <my-input v-model="searchQuery" placeholder="Search" style="width: 200px;d"/>    

        <my-dialog v-model:show="dialogVisible" >
            <post-form @create="createPost"/>
        </my-dialog>
        <my-select v-model="selectedSort" :options="sortOptions"/>   
    </div>
    
    
    <post-list 
    v-bind:posts="sortedAndSearchedPosts"
    v-on:remove ="removePost"
    v-if="!isPostLoading"
    />
    <div v-else>Loading...</div>
    <div class="page__wrapper">
        <div v-for="pageNumber in totalPages" :key="page" class="page" @click="changePage(pageNumber)" :class="{
            'current-page' : page === pageNumber
        }">{{ pageNumber }}</div>
    </div>
</div>

</template>

<script>
import  PostList  from "@/components/PostList.vue";
import  PostForm  from "./components/PostForm.vue";
import axios from 'axios';



export default {
    components:{
        PostList, PostForm
    },
    data() {
        return {
            posts: [],
            dialogVisible: false,
            isPostLoading: false,
            selectedSort: "",
            sortOptions: [
            {value:'title', name:'By name'},
            {value:'body', name:'By content'}
            ],
            searchQuery: "",
            page: 1,
            limit: 10,
            totalPages: 0,
        }
    },
    methods:{
        createPost(post){
            this.posts.push(post);
            this.dialogVisible = false;
            
        },
        removePost(post) {
            this.dialogVisible = false;
            this.posts = this.posts.filter(p => p.id !== post.id)
        },
        showDialog() {
            this.dialogVisible = true;
        },
        async fetchPosts() {
            try{
                this.isPostLoading = true
                setTimeout(async () => {
                    const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
                        params: {
                            _page: this.page,
                            _limit: this.limit
                        }
                    });
                    this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit)
                    this.posts = response.data; 
                    this.isPostLoading = false

                }, 1000)
               
            }catch (e) {
                alert('Error')
            } finally {
            }
        },
        changePage(pageNumber) {
            this.page = pageNumber
            this.fetchPosts()
        }
        
        
    },
    mounted() {
            this.fetchPosts();
        },
    // watch: {
    //     selectedSort(newValue){
    //         this.posts.sort((a,b) => {
    //             return a[this.selectedSort]?.localeCompare(b[this.selectedSort])
    //         })
    //     }
    // },
    computed: {
        sortedPosts() {
            return [...this.posts].sort((post1,post2) => post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]))
        },
        sortedAndSearchedPosts() {
            return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
        }
    }
}
</script>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
.app{
    padding: 20px;
}

.btn_form_dialog {
    margin: 20px;
    margin-left: 0;
}

.app_btns {
    display: flex;
    justify-content: space-between;
}

.page__wrapper {
    display: flex;
    margin-top: 15px;
}

.page {
    border: 1px solid black;
    padding: 10px;
}

.current-page {
    border: 2px solid green;
}
</style>