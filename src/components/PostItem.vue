<template>
    <div class="post">
        <div>
            <div><strong>Название:</strong>{{ post.title }}</div>
            <div><strong>Описание:</strong>{{ post.body }}</div>
        </div>
        <div class="post__btns">
            <my-button @click = "this.$emit('removePost', post)">Удалить</my-button>
        </div>
    </div>
</template>

<script>

export default {
    props: {
        post: {
            type: Object,
            required: true,
        }
    },
}
</script>

<style  scoped>
.post {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem;
    border: 2px solid teal;
}
</style>