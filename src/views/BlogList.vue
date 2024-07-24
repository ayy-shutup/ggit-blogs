<template>
    <div>

        <h1>Blogul GGIT Gulag</h1>
<div class="blogPost" >
    <input v-model="user"/>
    <select v-model="tag">
        <option value="gen">General</option>
        <option value="flm">Flame</option>
        <option value="rec">Recommended</option>
    </select><br>

    <textarea v-model="post"></textarea> <br>
    <button @click="submitFormHandler">Save post</button>
</div>
        <div v-if="blogList.length > 0">
            <BlogItem v-for="blog in blogList"
            :key="blog.id"
            :id="blog.id"
            :user="blog.user"
            :post="blog.post"
            :likes="blog.likes"
            :tag="blog.tag"
            @like="likeHandler($event)"
            @dislike="dislikeHandler($event)"/>

        </div>

        <div v-else>
            <p>Nici un post nu a fost creat</p>
        </div>
    </div>
</template>

<script>
import { myaxios } from '../axios';
import BlogItem from '../components/BlogItem.vue';
    export default {
        components: { BlogItem},
        data() {
            return {
                user: "Username",
                post: "",
                tag: "gen",
                blogList: []
            }
        },
        methods: {
            submitFormHandler() {
                const newBlog = {
                    user: this.user,
                    post: this.post,
                    tag: this.tag
                }   
                
                myaxios.post("/blog", newBlog).then((response) =>{
                    this.blogList = response.data.blogs
                })
                console.log(newBlog)
            },

            fetchBlogPosts() {
                myaxios.get("/blog").then (
                    (response) => {
                        console.log(response.data.blogs)
                        this.blogList = response.data.blogs
                    }
                )
            },

            likeHandler(event){
                console.log(event.itemID)
                myaxios.post(`/blog/${event.itemID}/like`).then((response) => {
                        console.log(response.data.blogs)
                        this.blogList = response.data.blogs
                    })
            },
            dislikeHandler(event){
                console.log(event.itemID)
                myaxios.post(`/blog/${event.itemID}/dislike`).then((response) => {
                        console.log(response.data.blogs)
                        this.blogList = response.data.blogs
                    })
            }
        },

        mounted () {
            this.fetchBlogPosts();
        },

        created () {
            this.fetchBlogPosts();
        }
        
    }
</script>

<style scoped>
</style>