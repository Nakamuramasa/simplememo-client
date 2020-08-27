<template>
    <div class="container">
        <base-article
            v-for="article in articles"
            :key="article.id"
            :article="article"
            @deleted="handleDelete"
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
        },
        handleDelete(id){
            this.articles = this.articles.filter(r => r.id !== id);
        }
    }
};
</script>
