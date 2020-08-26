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
                                    <input
                                        type="text"
                                        v-model="form.email"
                                        name="email"
                                        class="form-control"
                                        :class="{ 'is-invalid': form.errors.has('email') }"
                                        placeholder="メールアドレス"
                                    />
                                    <has-error :form="form" field="email"></has-error>
                                </div>
                                <div class="md-form">
                                    <input
                                        type="password"
                                        v-model="form.password"
                                        name="password"
                                        class="form-control"
                                        :class="{ 'is-invalid': form.errors.has('password') }"
                                        placeholder="パスワード"
                                    />
                                    <has-error :form="form" field="password"></has-error>
                                </div>
                                <base-button></base-button>
                                <!-- <button
                                    type="submit"
                                    :disabled="form.busy"
                                    class="btn btn-block blue-gradient mt-2 mb-2"
                                >
                                    <span v-if="form.busy">
                                        <i class="fas fa-spinner fa-spin"></i>
                                    </span>
                                    ログイン
                                </button> -->
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
