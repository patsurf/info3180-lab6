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
 </ul>
</template>
<script>
export default {
 data() {
 return {};
 },
};
<script>
import NewsList from '@/components/NewsList.vue'
export default {
 data() {
 return {
 articles: []
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
