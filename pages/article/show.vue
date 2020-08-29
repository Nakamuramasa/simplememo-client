<template>
    <div class="container">
        <base-article
            :article="article"
        ></base-article>
    </div>
</template>

<script>
export default {
    async asyncData({ $axios, params, error, redirect }){
        try{
            const article = await $axios.$get(`/articles/${params.id}`);
            return { article: article.data };
        }catch(err){
            if(err.response.status === 404){
                error({statusCode: 404, message: "投稿が見つかりませんでした。"})
            }else{
                error({statusCode: 500, message: "Internal server error"})
            }
        }
    }
};
</script>
