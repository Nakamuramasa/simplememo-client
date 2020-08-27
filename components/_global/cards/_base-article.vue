<template>
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
                <a class="text-dark" :href="`/articles/${article.id}`">
                    {{ article.title }}
                </a>
            </h3>
            <div class="card-text">
                {{ article.body }}
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        article: {
            type: Object,
            required: true
        }
    },
    methods: {
        destroyArticle(){
            this.$axios.delete(`/article/${this.article.id}`)
            .then(res => this.$emit('deleted', this.article.id))
            .catch(e => console.log(e))
        }
    }
};
</script>
