<script>
    // Import BlogPost component
    import blogPost2 from './subcomponents/BlogPost2.vue'
	import axios from 'axios'
    export default {
        data() {
            return {
                posts: [] // array of post objects
            }  
        },
        computed: {
            baseUrl() {
                if (window.location.hostname=='localhost')
                    return 'http://localhost:3000' 
                else {
                    const codespace_host = window.location.hostname.replace('5173', '3000')
                    return `https://${codespace_host}`;
                }
            }
        },
        created() { // created is a hook that executes as soon as Vue instance is created
            axios.get(`${this.baseUrl}/posts`)
            .then(response => {
                // this gets the data, which is an array
                this.posts = response.data
                console.log(response.data)
            })
            .catch(error => {
                this.posts = [{ entry: 'There was an error: ' + error.message }]
            })
        },
        components:{
            blogPost2
        },
        methods:{
            deletePost(id){
                console.log(id)
                axios.get(`${this.baseUrl}/deletePost`,{params:{
                    "id":id
                }})
                .then(response => {
                    console.log(response.data)
                })
                .catch(error => {
                    console.log(error.message)
                })
            }
        }
        
    }
</script>

<template>
   <!-- TODO: make use of the 'blog-post' component to display the blog posts -->
    <blogPost2
        v-for="post in posts"
        :key="post.id"
        :subject="post.subject"
        :mood="post.mood"
        :entry="post.entry"
    >
    <button @click="deletePost(post.id)" class="btn btn-primary">Delete</button>
    </blogPost2>
</template>

