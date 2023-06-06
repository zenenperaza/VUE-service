<template>
    <div class="post-container">
       <div class="post-card">
        <h3>{{ post.title }}</h3>
        <p>{{ post.body }}</p>
       </div>
    </div>
    <router-link v-bind:to="{name: 'PostList'}" class="link">Return Back</router-link>
</template>

<script lang="ts" setup>
import PostService from '@/services/PostService';
import { onMounted } from "vue";
import { useRoute } from "vue-router";

const service = new PostService()
const post = service.getPost()

onMounted(async () => {
    const route = useRoute()
    let elm = route.params.id
    await service.fetchById(elm)
})

</script>

<style lang="scss" scoped> 
.post-container{
    width: 100vw;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
}
.post-card{
    padding: 25px;
    width: 700px;
    border-radius: 15px;
    border: 1px solid #ccc;

}
.link {
margin-top: 30px;
color: $primaryColor;
text-decoration: none;
}
.link:hover{
    text-decoration: underline;
}

</style>