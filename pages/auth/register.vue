<template>
    <div class="container">
        <div class="row">
            <div class="mx-auto col col-12 col-sm-11 col-md-9 col-lg-7 col-xl-6">
                <div class="card mt-3">
                    <div class="card-body text-center">
                        <h2 class="h3 card-title text-center mt-2">ユーザー登録</h2>
                        <div class="card-text">

                            <form @submit.prevent="submit">
                                <alert-success :form="form">
                                    アカウント認証用メールを送信しました。
                                </alert-success>
                                <div class="md-form">
                                    <base-input
                                        :form="form"
                                        field="username"
                                        v-model="form.username"
                                        placeholder="ユーザー名"
                                    ></base-input>
                                </div>
                                <div class="md-form">
                                    <base-input
                                        :form="form"
                                        field="name"
                                        v-model="form.name"
                                        placeholder="フルネーム"
                                    ></base-input>
                                </div>
                                <div class="md-form">
                                    <base-input
                                        :form="form"
                                        field="email"
                                        inputType="email"
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
                                <div class="md-form">
                                    <base-input
                                        :form="form"
                                        field="password_confirmation"
                                        inputType="password"
                                        v-model="form.password_confirmation"
                                        placeholder="パスワード(確認)"
                                    ></base-input>
                                </div>
                                <base-button :loading="form.busy">
                                    ユーザー登録
                                </base-button>
                            </form>

                            <div class="mt-0">
                                <nuxt-link to="/login" class="card-text">ログインはこちら</nuxt-link>
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
                usename: '',
                name: '',
                email: '',
                password: '',
                password_confirmation: ''
            })
        }
    },
    methods: {
        submit(){
            this.form.post(`/register`)
            .then(res => {
                this.form.reset();
            }).catch(error => {
                console.log(error);
            });
        }
    }
};
</script>
