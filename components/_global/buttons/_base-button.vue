<template>
    <button
        :class="type"
        :type="nativeType"
        :disabled="loading"
    >
        <span v-if="loading">
            <i class="fas fa-spinner fa-spin"></i>
        </span>
        <slot />
    </button>
</template>

<script>
export default {
    name: 'base-button',
    props:{
        type: {
            type: String,
            default: 'btn btn-block blue-gradient mt-2 mb-2'
        },
        nativeType: {
            type: String,
            default: 'submit'
        },
        loading: {
            type: Boolean,
            default: false
        }
    }
};
</script>
