<template>
<form @submit.prevent="searchNews" class="d-flex flex-column justify-content-center">
        <div class="input-group mx-sm-3 mb-1">
            <label class="visually-hidden" for="search">Search </label>
            <input type="search" name="search" v-model="searchTerm"
            id="search" class="form-control mb-2 mr-sm-2" placeholder="Enter
            search term here" />
            <button class="btn btn-primary mb-2">Search</button>
        </div>
        <p>You are searching for {{ searchTerm }}</p>
    </form>
   

  <div class="card_container">
        <div v-for="(article,index) in articles"  :key="index" class="card" style="width: 18rem;">
        <img :src="article.urlToImage" class="card-img-top">
        <div class="card-body">
            <h5 class="card-title">{{ article.title }}</h5>
            <p class="card-text">{{article.description}}</p>
        </div>
    </div>
  </div>
</template>


<script>
    export default {
        data() {
            return {
                articles:[],
                searchTerm: ''
            };
        },
        created() {
            let self = this;
            fetch('https://newsapi.org/v2/top-headlines?country=us',
            {
            headers: {
                'Authorization': `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`
            }
            })
            .then(function(response) {
                return response.json();
            })
            .then(function(data) {
                console.log(data);
                self.articles=data.articles;
            });
        },
        methods: {
            searchNews() {
                let self = this;
                fetch('https://newsapi.org/v2/everything?q='+
                self.searchTerm + '&language=en', {
                headers: {
                'Authorization': `Bearer $
                {import.meta.env.VITE_NEWSAPI_TOKEN}`,
                }
                })
                .then(function(response) {
                return response.json();
                })
                .then(function(data) {
                console.log(data);
                self.articles = data.articles;
                });
                }
            }
    }
</script>

<style scoped>
    .card_container{
    display:grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-rows: auto;
    gap:10px;
    }
</style>
