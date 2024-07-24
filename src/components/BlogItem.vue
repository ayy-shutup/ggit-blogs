<template>
    <div class="blogPost" >
        <h5>{{ user }}</h5>
        <p>{{ post }}</p>

        <div class="likes">
            <button @click="likeItem">Like</button>
            <p>{{ likes }}</p>
            <button @click="dislikeItem">Dislike</button>
            <button @click="deletePost">Delete</button>
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            user: String,
            post: String,
            likes: Number,
            tag: String,
            id: Number
        },

        emits: ['like', 'dislike', 'delete'],
        methods: {
            likeItem(){
            this.$emit("like", {itemID: this.id})
            },
            dislikeItem(){
            this.$emit("dislike", {itemID: this.id})
            },
            deletePost(){
                this.$emit("delete", {itemID: this.id})
            }
        }
    }
</script>
<style scoped>
.blogPost {
    padding: 12px 20px 20px 30px;
    inline-size: 100px;
    min-width: 400px;
    max-width: 500px;
    min-height: min-content;
    max-height: calc(300px + 20%);
    overflow-wrap: anywhere;
    overflow-x: hidden;
    border-width: 1px 2px 4px 2px;
    margin-top: 50px;
    border-color: rgb(79, 45, 47);
    border-style: solid;
    border-radius: 7px;
    background-color: rgb(230, 215, 221);
}

.likes {
    padding-bottom: 40px;
}
</style>