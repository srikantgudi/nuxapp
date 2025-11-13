<template>
    <div>
        <h2>Comments</h2>
        <div class="data-list">
            <Comments :comments />
        </div>
    </div>
</template>

<script setup>
    import { ref, onMounted } from 'vue';
    import Comments from '@/components/comments.vue';
    const comments = ref([]);
    onMounted(async () => {
        const response = await fetch('https://jsonplaceholder.typicode.com/comments');
        comments.value = await response.json();
    });
</script>