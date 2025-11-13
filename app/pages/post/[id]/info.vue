<template>
    <div style="margin:1vh 5vw">
        <div><router-link to="/posts">[&laquo; back to list]</router-link></div>
        <h2>Post : {{info.title}}</h2>
        <div>{{info.body}}</div>
    </div>
</template>

<script setup>
    import { onMounted } from 'vue';
    import { useRoute } from 'vue-router';
    const route = useRoute();
    const infoUrl = `https://jsonplaceholder.typicode.com/posts/${route.params.id}`;
    const response = await fetch(infoUrl);
    const info = await response.json();
</script>