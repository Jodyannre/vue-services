<template>
    <div>
        <h1>Listado de posts</h1>
        <ul class="post-list">
            <li v-for="post in posts" :key="post.id">
                <router-link :to="({name:'PostDetail', params:{id:post.id}})">
                    {{ post.title }}
                </router-link>
            </li>
        </ul>
    </div>
</template>
  
<script lang="ts" setup>
    //Composition API 
    /*
    import { defineComponent, onMounted } from 'vue';
    import PostService from '@/services/PostServices';

    export default defineComponent({
        name: 'PostList',
        setup() {
            const service = new PostService();
            const posts  = service.getPosts();

            onMounted(async ()=>{
                await service.fetchAll();
            })
            return {posts};
        },
    });
    */

   // Options API -- tambien modificar el for y poner posts.value
   /*
   import { defineComponent } from 'vue';
    import PostService from '@/services/PostServices';

    export default defineComponent({
        name: 'PostList',
        data() {
            const service = new PostService()
            const posts  = service.getPosts()
            return {posts, service};
        },
        async mounted() {
            await this.service.fetchAll()
        },
    });
    */

    // Composition API con setup
    import { onMounted, ref, Ref } from 'vue';
    import PostService from '@/services/PostServices';

    const service = new PostService();
    const posts  = service.getPosts();


    onMounted(async ()=>{
        await service.fetchAll();
    })


</script>
  
<style scoped lang="scss">

    .post-list {
        width: 95vw;
        height: 75px;
        padding: 20px;
        list-style-type: none;
        color: red;

        li {
        padding: 10px;
        width: 100%;
        border: 1px solid #ccc;

        a {
            text-decoration: none;
            color: $textColor; 
            cursor: pointer;
        }
        }

        a:hover {
            color:$primaryColor;
        }
    }
</style>