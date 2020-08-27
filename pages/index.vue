<template>
    <div class="container">
        <base-article
            v-for="article in articles"
            :key="article.id"
            :article="article"
        ></base-article>
    </div>
</template>

<script>
export default {
    data(){
        return {
            articles: []
        }
    },
    created(){
        this.fetchArticles();
    },
    methods:{
        async fetchArticles(){
            const {data} = await this.$axios.$get('/articles');
            this.articles = data;
        }
    }
};
</script>
