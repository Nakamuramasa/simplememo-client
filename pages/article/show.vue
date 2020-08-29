<template>
    <div class="container">
        <div class="card mt-3">
            <div class="card-body d-flex flex-row">
                <i class="fas fa-user-circle fa-3x mr-1"></i>
                <div>
                    <div class="font-weight-bold">
                        {{ article.user.username }}
                    </div>
                    <div class="font-weight-lighter">
                        {{ article.created_at_dates.created_at }}
                    </div>
                </div>

                <div class="ml-auto card-text" v-if="$auth.loggedIn && $auth.user.id === article.user.id">
                    <div class="dropdown">
                        <a data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                            <button type="button" class="btn btn-link text-muted m-0 p-2">
                                <i class="fas fa-ellipsis-v"></i>
                            </button>
                        </a>
                        <div class="dropdown-menu dropdown-menu-right">
                            <a class="dropdown-item" :href="`/articles/${article.id}/edit`">
                                <i class="fas fa-pen mr-1"></i>記事を更新する
                            </a>
                            <div class="dropdown-divider"></div>
                            <a @click.prevent="destroyArticle" class="dropdown-item text-danger">
                                <i class="fas fa-trash-alt mr-1"></i>記事を削除する
                            </a>
                        </div>
                    </div>
                </div>

            </div>
            <div class="card-body pt-0 pb-2">
                <h3 class="h4 card-title">
                    {{ article.title }}
                </h3>
                <div class="card-text">
                    {{ article.body }}
                </div>
            </div>
            <div class="card-body pt-0 pb-2 pl-3">
                <div class="card-text">
                    <div>
                        <button
                            type="button"
                            class="btn m-0 p-1 shadow-none"
                        >
                            <i class="fas fa-heart mr-1" />
                        </button>
                        {{ article.likes_count }}
                    </div>
                </div>
            </div>

            <div class="card-body pt-0 pb-4 pl-3">
                <div class="card-text line-height">
                    <a
                        class="border p-1 mr-1 mt-1 text-muted"
                        v-for="(tag, i) in article.tag_list.tags"
                        :key="`tag-${i}`"
                        :href="`/tags/${article.tag_list.normalized[i]}`"
                    >{{ tag }}</a>
                </div>
            </div>

        </div>
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
    },
    methods: {
        destroyArticle(){
            this.$axios.delete(`/article/${this.article.id}`)
            .then(res => {
                setTimeout(() => {
                    this.$router.push({ name: 'index' })
                }, 2000);
            })
            .catch(e => console.log(e))
        }
    }
};
</script>
