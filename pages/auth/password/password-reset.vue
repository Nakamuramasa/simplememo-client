<template>
    <div class="container">
        <div class="row">
            <div class="mx-auto col col-12 col-sm-11 col-md-9 col-lg-7 col-xl-6">
                <div class="card mt-3">
                    <div class="card-body text-center">
                        <h2 class="h3 card-title text-center mt-2">パスワードリセット</h2>
                        <div class="card-text">

                            <form @submit.prevent="submit">
                                <alert-success :form="form">
                                    {{ status }}
                                    <nuxt-link to="/login">ログイン画面へ</nuxt-link>
                                </alert-success>
                                <div class="md-form">
                                    <base-input
                                        :form="form"
                                        :readonly="true"
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
                                        placeholder="新しいパスワード"
                                    ></base-input>
                                </div>
                                <div class="md-form">
                                    <base-input
                                        :form="form"
                                        field="password_confirmation"
                                        inputType="password"
                                        v-model="form.password_confirmation"
                                        placeholder="新しいパスワード(確認)"
                                    ></base-input>
                                </div>
                                <base-button :loading="form.busy">
                                    パスワードリセット
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
    data(){
        return {
            status: '',
            form: this.$vform({
                email: '',
                password: '',
                password_confirmation: '',
                token: ''
            })
        };
    },
    created(){
        this.form.email = this.$route.query.email
        this.form.token = this.$route.params.token
    },
    methods: {
        submit(){
            this.form.post('/password/reset')
            .then(res => {
                this.status = res.data.status;
                this.form.reset();
            })
            .catch(e => {
                console.log(e);
            });
        }
    }
};
</script>
