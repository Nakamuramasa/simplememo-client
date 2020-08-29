<template>
    <div class="card-body pt-0 pb-4 pl-3">
        <div class="card-text line-height">
            <a
                class="border p-1 mr-1 mt-1 text-muted"
                v-for="(tag, i) in article.tag_list.tags"
                :key="`tag-${i}`"
                :href="`/tags/${article.tag_list.normalized[i]}`"
            >{{ tag }}</a>
        </div>
    </div>
</template>

<script>
export default {
    props:['article']
};
</script>
