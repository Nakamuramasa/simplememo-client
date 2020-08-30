<template>
    <div class="container">
        <div class="card mt-3">
            <div class="card-body">
                <div class="d-flex flex-row">
                    <a href="#" class="text-dark">
                        <i class="fas fa-user-circle fa-3x"></i>
                    </a>

                    <UserFollow
                        v-if="$auth.loggedIn"
                        :user="user"
                    ></UserFollow>
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

        <DetailArticle :user="user" />

    </div>
</template>

<script>
import UserFollow from '@/components/UserFollow';
import DetailArticle from '@/components/DetailArticle';
export default {
    components: {
        UserFollow,
        DetailArticle
    },
    data(){
        return {
            user: []
        }
    },
    created(){
        this.userArticles();
    },
    methods:{
        async userArticles(){
            const {data} = await this.$axios.$get(`/user/${params.id}`);
            this.user = data;
        }
    }
};
</script>
