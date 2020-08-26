<template>
    <div class="container">
        <div class="row">
            <div class="mx-auto col col-12 col-sm-11 col-md-9 col-lg-7 col-xl-6">
                <div class="card mt-3">
                    <div class="card-body text-center">
                        <h2 class="h3 card-title text-center mt-2">パスワードリセット</h2>
                        <div class="card-text">

                            <form @submit.prevent="submit">
                                <alert-success :form="form">{{ status }}</alert-success>
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
    data(){
        return {
            status: '',
            form: this.$vform({
                email: ''
            })
        }
    },
    methods: {
        submit(){
            this.form.post('/password/email')
            .then(res => {
                this.status = res.data.status;
                this.form.reset();
            }).catch(e => {
                console.log(e)
            })
        }
    }
};
</script>
