<script>
export default {
    data() {
        return {
            message: "Hello World! Welcome to VueJS"
        };
    },
}
</script>

<template>
    <div class="container">
      <div class="text-center">
        <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />
        <h1>{{ message }}</h1>
      </div>
    </div>
</template>

<style>
 export default {
     data() {…},
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
</style>
