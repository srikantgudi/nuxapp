<template>
    <div>
        <div style="margin-bottom: 1rem;"><router-link to="/posts">[&laquo; back to list]</router-link></div>
        <div class="para-title">POST:</div>
        <div style="margin:1vh 2vw">
            <div><b>{{post.title}}</b></div>
            <div>{{post.body}}</div>
        </div>
        <div class="para-title">Comments for post</div>
        <div>
            <Comments :comments />
        </div>
    </div>
</template>

<script setup>
    import { onMounted } from 'vue';
    import { useRoute } from 'vue-router';
    const route = useRoute();
    const comments = ref([]);
    const post = ref({});
    onMounted(async () => {
        const postId = route.params.id;
        const postUrl = `https://jsonplaceholder.typicode.com/posts/${postId}`;
        const resPost = await fetch(postUrl);
        post.value = await resPost.json();
        const infoUrl = `https://jsonplaceholder.typicode.com/comments`;
        const resComment = await fetch(infoUrl);
        comments.value = await resComment.json();
    });
</script>