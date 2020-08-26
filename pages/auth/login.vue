<template>
    <div class="container">
        <div class="row">
            <div class="mx-auto col col-12 col-sm-11 col-md-9 col-lg-7 col-xl-6">
                <div class="card mt-3">
                    <div class="card-body text-center">
                        <h2 class="h3 card-title text-center mt-2">ログイン</h2>
                        <div class="card-text">

                            <form @submit.prevent="submit">
                                <alert-error v-if="form.errors.has('message')" :form="form">
                                    {{ form.errors.get('message') }}
                                    <nuxt-link to="/verification/resend">認証メールの再送信</nuxt-link>
                                </alert-error>
                                <div class="md-form">
                                    <base-input
                                        :form="form"
                                        field="email"
                                        v-model="form.email"
                                        placeholder="メールアドレス"
                                    ></base-input>
                                </div>
                                <div class="md-form">
                                    <base-input
                                        :form="form"
                                        field="password"
                                        inputType="password"
                                        v-model="form.password"
                                        placeholder="パスワード"
                                    ></base-input>
                                </div>
                                <base-button :loading="form.busy">
                                    ログイン
                                </base-button>
                            </form>

                            <div class="mt-0">
                                <nuxt-link to="/register" class="card-text">ユーザー登録はこちら</nuxt-link>
                            </div>
                            <div class="mt-2">
                                <nuxt-link to="/password/email" class="card-text">パスワードを忘れた</nuxt-link>
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
    data(){
        return {
            form: this.$vform({
                email: '',
                password: ''
            })
        }
    },
    methods:{
        submit(){
            this.$auth
            .loginWith('local', {
                data: this.form
            }).then(res => {
                console.log(res)
            }).catch(e => {
                this.form.errors.set(e.response.data.errors);
            });
        }
    }
};
</script>
