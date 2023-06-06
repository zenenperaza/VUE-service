<template>
<div > 
<h1 class="btn btn-danger">Listado de Post</h1>
<ul class="post-list">
    <li v-for="post in posts" v-bind:key="post.id">
        <router-link v-bind:to="{name: 'PostDetail', params: {id: post.id}}">
        {{ post.title }}
        </router-link>
    </li>
</ul>
</div>
</template>

<script lang="ts" setup>
import PostService from "@/services/PostService";
import { onMounted } from "vue";

    const service = new PostService()
    const posts = service.getPosts()

    onMounted(async () => {
        await service.fetchAll()
    })


</script>
<!-- COMPOSITION API CON SETUP -->
<!-- <script lang="ts">
import PostService from "@/services/PostService";
import { defineComponent, onMounted } from "vue";

export default defineComponent({
    name:"postList",
    setup(){
        const service = new PostService()
        const posts = service.getPost()

        onMounted(async () => {
            await service.fetchAll()
        })
        return {posts}
    }
})
</script> -->

<style scoped lang="scss">
.post-list {
    list-style: none;
    padding: 10px;
    width: 100%;
    height: 75px;

    li {
    padding: 3px;
    text-align-last: left;
    margin: 5px;
    border-bottom: 1px blue solid;
    width: 100%;
    color: #ccc;
    cursor: pointer;

    a{
        text-decoration: none;
        color: #ccc;
        cursor: pointer;
    }

    a:hover{
        color: $primaryColor;
    }
   

    }

}

</style>