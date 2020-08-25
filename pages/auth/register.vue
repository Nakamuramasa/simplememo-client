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
                                    <input
                                        type="text"
                                        v-model="form.username"
                                        name="username"
                                        class="form-control"
                                        :class="{ 'is-invalid': form.errors.has('username') }"
                                        placeholder="ユーザー名"
                                    />
                                    <has-error :form="form" field="username"></has-error>
                                </div>
                                <div class="md-form">
                                    <input
                                        type="text"
                                        v-model="form.name"
                                        name="name"
                                        class="form-control"
                                        :class="{ 'is-invalid': form.errors.has('name') }"
                                        placeholder="フルネーム"
                                    />
                                    <has-error :form="form" field="name"></has-error>
                                </div>
                                <div class="md-form">
                                    <input
                                        type="email"
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
                                <div class="md-form">
                                    <input
                                        type="password"
                                        v-model="form.password_confirmation"
                                        name="password_confirmation"
                                        class="form-control"
                                        placeholder="パスワード(確認)"
                                    />
                                </div>
                                <button
                                    type="submit"
                                    :disabled="form.busy"
                                    class="btn btn-block blue-gradient mt-2 mb-2"
                                >
                                    <span v-if="form.busy">
                                        <i class="fas fa-spinner fa-spin"></i>
                                    </span>
                                    ユーザー登録
                                </button>
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
