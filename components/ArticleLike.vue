<template>
    <div class="card-body pt-0 pb-2 pl-3">
        <div class="card-text">
            <div>
                <a href="#" class="btn m-0 p-1 shadow-none" @click.prevent="likeIt">
                    <template  v-if="liked">
                        <span>
                            <i class="fas fa-heart mr-1 red-text" />
                        </span>
                    </template>
                    <template v-else>
                        <span>
                            <i class="fas fa-heart mr-1" />
                        </span>
                    </template>
                </a>
                {{ count }}
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props:['article'],
    data() {
        return {
            liked: this.article.liked,
            count: this.article.likes_count
        }
    },
    methods: {
        likeIt(){
            if(this.$auth.loggedIn){
                this.liked ? this.decr() : this.incr()
                this.liked = !this.liked
            }
        },
        incr(){
            this.$axios.post(`/articles/${this.article.id}/like`)
            .then(res => this.count++);
        },
        decr(){
            this.$axios.post(`/articles/${this.article.id}/like`)
            .then(res => this.count--);
        }
    }
};
</script>
