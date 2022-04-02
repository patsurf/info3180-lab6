<template>
 <ul class="news__list">
 <li class="news__item">News item 1</li>
 <li class="news__item">News item 2</li>
 <li class="news__item">News item 3</li>
 </ul>
<template>
 <ul class="news__list">
 <li v-for="article in articles"
class="news__item">{{ article.title }}</li>
<form @submit.prevent="searchNews" class="d-flex flex-column justify-content-center">
 <div class="input-group mx-sm-3 mb-2">
 <label class="visually-hidden" for="search">Search</
label>
 <input type="search" name="search" v-model="searchTerm"
id="search" class="form-control mb-2 mr-sm-2" placeholder="Enter
search term here" />
 <button class="btn btn-primary mb-2">Search</button>
 </div>
 <p>You are searching for {{ searchTerm }}</p>
 </form>
 </ul>
</template>
<script>
export default {
 data() {
 return {};
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
};
<script>
import NewsList from '@/components/NewsList.vue'
export default {
 data() {
 return {
 articles: []
 searchTerm: ''
 }
 },
 components: { NewsList }
}
created() {
let self = this;
 fetch('https://newsapi.org/v2/top-headlines?country=us',
{
 headers: {
 'Authorization': 'Bearer <your-api-token>'
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
</script>
