<template>
    <div class="container">
        <div class="row">
            <div class="col-12">
                <div class="card mt-3">
                    <div class="card-body pt-0">
                        <div class="card-text">

                            <form @submit.prevent="submit">
                                <alert-success :form="form">
                                    投稿しました。
                                </alert-success>
                                <div class="md-form">
                                    <div class="md-form">
                                        <base-input
                                            :form="form"
                                            field="title"
                                            v-model="form.title"
                                            placeholder="タイトル"
                                        ></base-input>
                                    </div>
                                </div>
                                <div class="form-group">
                                    <client-only>
                                        <input-tag
                                            v-model="form.tags"
                                            placeholder="タグを追加"
                                        ></input-tag>
                                    </client-only>
                                </div>
                                <div class="form-group">
                                    <label></label>
                                    <base-textarea
                                        :form="form"
                                        field="body"
                                        v-model="form.body"
                                        placeholder="本文"
                                    ></base-textarea>
                                </div>
                                <base-button :loading="form.busy">
                                    投稿する
                                </base-button>
                            </form>

                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    middleware: ['auth'],
    data(){
        return {
            form: this.$vform({
                title: '',
                tags: [],
                body: ''
            })
        };
    },
    async asyncData({ $axios, params, error, redirect }){
        try{
            const article = await $axios.$get(`/articles/${params.id}/byUser`);
            return { article: article.data };
        }catch(err){
            if(err.response.status === 404){
                error({statusCode: 404, message: "投稿が見つかりませんでした。"})
            }else{
                error({statusCode: 500, message: "Internal server error"})
            }
        }
    },
    mounted(){
        Object.keys(this.form).forEach(key => {
            if(this.article.hasOwnProperty(key)){
                this.form[key] = this.article[key];
            }
        });
        this.form.tags = this.article.tag_list.tags || []
    },
    methods: {
        submit(){
            this.form.put(`/article/${this.$route.params.id}`)
            .then(res => {
                setTimeout(() => {
                    this.$router.push({ name: 'index' })
                }, 2000);
            })
            .catch(err => console.log(err.response));
        }
    }
};
</script>
