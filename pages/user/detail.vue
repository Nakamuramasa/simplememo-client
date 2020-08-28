<template>
    <div class="container">
        <div class="card mt-3">
            <div class="card-body">
                <div class="d-flex flex-row">
                    <a href="#" class="text-dark">
                        <i class="fas fa-user-circle fa-3x"></i>
                    </a>

                    <follow-button
                        class="ml-auto"
                        v-if="$auth.loggedIn"
                    ></follow-button>
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
        <ul class="nav nav-tabs nav-justified mt-3">
            <li class="nav-item">
                <a class="nav-link text-muted active" href="#">
                    記事
                </a>
            </li>
            <li class="nav-item">
                <a class="nav-link text-muted" href="#">
                    いいね
                </a>
            </li>
        </ul>
        <div v-for="article in articles">
            {{ article.title }}
        </div>
    </div>
</template>

<script>
import FollowButton from '@/components/FollowButton';
export default {
    components: {
        FollowButton
    },
    async asyncData({ $axios, params, error, redirect }){
        try{
            const user = await $axios.$get(`/user/${params.id}`);
            return { user: user.data, articles: user.data.articles };
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
