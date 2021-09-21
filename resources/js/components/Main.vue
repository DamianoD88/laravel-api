<template>
    <div class="container">
        <p>Current page {{ currentPage }} - Last Page {{ lastPage }}</p>
        <div class="row">
            <div class="col-sm-6" v-for="post in posts" :key="post.id">
                <div class="card">
                    <div class="card-body">
                        <h5 class="card-title">{{ post.title }}</h5>
                        <p class="card-text">{{ post.content }}</p>
                        <a href="#" class="btn btn-primary">Details</a>
                    </div>
                </div>
             </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "Main",
    data(){
        return {
            chiamataApi: 'http://localhost:8000/api/posts',
            posts: [],
            currentPage: 1,
            lastPage: 4
        }
    },
    created(){
        // this.stampaAugurio();
        // console.log('chiamataApi');
        this.getPosts();
    },
    methods: {
        // stampaAugurio(){
        //     console.log('Buonanotte');
        // }
        getPosts(){
            axios.get(this.chiamataApi)
                .then(response => {
                    
                    this.posts = response.data.results.data;
                    this.currentPage = response.data.results.current_page;
                    this.lastPage = response.data.results.last_page;
                    console.log(this.posts);
                    console.log(response.data.results.current_page);
                    console.log(response.data.results.last_page);
                })
                .catch();
        }
    }
}
</script>

<style lang="scss" scoped>

</style>