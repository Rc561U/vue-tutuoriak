<template>

    <div v-if="posts.length > 0">
        <h3>List of users</h3>
        <transition-group name="post_list">
            <post-item 
             v-for="post in posts"
             :post="post" 
             :key="post.id"
             @remove="$emit('remove', post)"
             />
        </transition-group>
        
    </div>

    <h2 v-else>No posts</h2>
</template>
<script>
import PostItem from "@/components/PostItem"
export default {
    components: {PostItem},
    props: {
        posts: {
            type: Array,
            required: true
        }
    }
}

</script>
<style scoped>
.post_list-item {
  display: inline-block;
  margin-right: 10px;
}
.post_list-enter-active,
.post_list-leave-active {
  transition: all 0.5s ease;
}
.post_list-enter-from,
.post_list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}
.post_list-move {
  transition: transform 0.8s ease;
}

</style>