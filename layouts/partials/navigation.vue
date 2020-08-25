<template>
    <nav class="navbar navbar-expand navbar-dark blue-gradient">
        <nuxt-link to="/" class="navbar-brand"><i class="far fa-sticky-note mr-1"></i>memo</nuxt-link>
        <ul class="navbar-nav ml-auto">
            <template v-if="!$auth.loggedIn">
                <li class="nav-item">
                    <nuxt-link to="/register" class="nav-link">ユーザー登録</nuxt-link>
                </li>
                <li class="nav-item">
                    <nuxt-link to="/login" class="nav-link">ログイン</nuxt-link>
                </li>
            </template>
            <template v-else>
                <li class="nav-item">
                    <a class="nav-link" href=""><i class="fas fa-pen mr-1"></i>投稿する</a>
                </li>
                <li class="nav-item dropdown">
                    <a class="nav-link dropdown-toggle" id="navbarDropdownMenuLink" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                        <i class="fas fa-user-circle"></i>
                    </a>
                    <div class="dropdown-menu dropdown-menu-right dropdown-primary" aria-labelledby="navbarDropdownMenuLink">
                        <button class="dropdown-item" type="button" onclick="location.href=''">
                            マイページ
                        </button>
                        <div class="dropdown-divider"></div>
                        <button form="logout-button" class="dropdown-item" type="button" @click.prevent="logout">
                            ログアウト
                        </button>
                    </div>
                </li>
            </template>
        </ul>
    </nav>
</template>

<script>
export default {
    methods: {
        logout(){
            this.$auth.logout();
        }
    }
};
</script>
