<template>
    <div class="container">
        <div class="row">
            <div class="mx-auto col col-12 col-sm-11 col-md-9 col-lg-7 col-xl-6">
                <div class="card mt-3">
                    <div class="card-body text-center">
                        <h2 class="h3 card-title text-center mt-2">認証メールの再送信</h2>
                        <div class="card-text">

                            <form @submit.prevent="submit">
                                <alert-error v-if="form.errors.has('message')" :form="form">
                                    {{ form.errors.get('message') }}
                                </alert-error>
                                <alert-success :form="form">
                                    アカウント認証用メールを送信しました。
                                </alert-success>
                                <div class="md-form">
                                    <base-input
                                        :form="form"
                                        field="email"
                                        v-model="form.email"
                                        placeholder="メールアドレス"
                                    ></base-input>
                                </div>
                                <base-button :loading="form.busy">
                                    送信
                                </base-button>
                            </form>

                            <div class="mt-0">
                                <nuxt-link to="/login" class="card-text">ログイン画面へ戻る</nuxt-link>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    middleware: ['guest'],
    data(){
        return {
            form: this.$vform({
                email: ''
            })
        }
    },
    methods:{
        submit(){
            this.form
            .post(`/verification/resend`)
            .then(res => this.form.reset())
            .catch(e => console.log(e))
        }
    }
};
</script>
