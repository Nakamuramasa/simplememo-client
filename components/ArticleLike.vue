<template>
    <div class="card-body pt-0 pb-2 pl-3">
        <div class="card-text">
            <div>
                <button
                    type="button"
                    class="btn m-0 p-1 shadow-none"
                >
                    <i class="fas fa-heart mr-1" />
                </button>
                {{ article.likes_count }}
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props:['article']
};
</script>
