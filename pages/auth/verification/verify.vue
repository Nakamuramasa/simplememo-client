<template>
    <div class="container">
        <div class="row">
            <div class="mx-auto col col-12 col-sm-11 col-md-9 col-lg-7 col-xl-6">
                <div class="card mt-3">
                    <div class="card-body text-center">
                        <h2 class="h3 card-title text-center mt-2">アカウント認証</h2>
                        <div class="card-text">

                            <form>
                                <div class="form-group" v-if="success">
                                    <div class="alert alert-success">
                                        {{ status }}
                                    </div>
                                    <nuxt-link to="/login" class="card-text">ログイン画面へ</nuxt-link>
                                </div>
                                <div class="form-group" v-else>
                                    <div class="alert alert-danger">
                                        {{ status }}
                                    </div>
                                </div>
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
    async asyncData({ params, query, app }){
        const q = Object.keys(query).map(k => `${k}=${query[k]}`).join('&');
        try{
            const { data } = await app.$axios.post(`/verification/verify/${params.id}?${q}`);
            return { success: true, status: data.message };
        }catch(e){
            return { success: false, status: e.response.data.errors.message };
        }
    }
};
</script>
