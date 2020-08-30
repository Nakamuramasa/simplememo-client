<template>
    <div class="ml-auto">
        <button
            class="btn-sm shadow-none border border-primary p-2"
            :class="buttonColor"
            @click.prevnet="followIt"
        >
            <i class="mr-1" :class="buttonIcon"></i>
            {{ buttonText }}
        </button>
    </div>
</template>

<script>
export default {
    props:['user'],
    data() {
        return {
            followed: this.user.followed,
        }
    },
    computed: {
        buttonColor() {
            return this.followed ? 'bg-primary text-white' : 'bg-white'
        },
        buttonIcon() {
            return this.followed ? 'fas fa-user-check' : 'fas fa-user-plus'
        },
        buttonText() {
            return this.followed ? 'フォロー中' : 'フォロー'
        }
    },
    methods: {
        followIt(){
            if(this.$auth.loggedIn){
                this.$axios.post(`/users/${this.user.id}/follow`)
                .then(res => {
                    this.followed = !this.followed
                })
            }
        }
    }
};
</script>
