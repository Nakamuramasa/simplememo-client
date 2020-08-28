<template>
    <div class="container">
        <div class="card mt-3">
            <div class="card-body">
                <div class="d-flex flex-row">
                    <a href="#" class="text-dark">
                        <i class="fas fa-user-circle fa-3x"></i>
                    </a>
                </div>
                <h2 class="h5 card-title m-0">
                    <a href="#" class="text-dark">
                        {{ user.username }}
                    </a>
                </h2>
            </div>
            <div class="card-body">
                <div class="card-text">
                    <a href="" class="text-muted">
                        {{ user.follow }} フォロー
                    </a>
                    <a href="" class="text-muted">
                        {{ user.followers }} フォロワー
                    </a>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    async asyncData({ $axios, params, error, redirect }){
        try{
            const user = await $axios.$get(`/user/${params.id}`);
            return { user: user.data };
        }catch(err){
            if(err.response.status === 404){
                error({statusCode: 404, message: "ユーザーが見つかりませんでした。"})
            }else{
                error({statusCode: 500, message: "Internal server error"})
            }
        }
    }
};
</script>
