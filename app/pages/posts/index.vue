<template>
    <div>
        <div class="text-3xl pb-2 border-b-2">Posts</div>
        <div class="shadow-lg shadow-gray-400" style="height:80vh;overflow-y: auto;">
            <table class="w-full">
                <thead class="bg-gray-800 text-gray-200 sticky top-0">
                    <tr>
                        <td class="p-1 w-10 text-right">Id</td>
                        <td class="p-1 w-20 text-right">User-Id</td>
                        <td class="p-1 w-120">Title</td>
                        <td class="p-1 w-auto">Body</td>
                    </tr>
                </thead>
                <tbody>
                    <tr class="align-top even:bg-gray-200" v-for="post in posts.value" :key="post.id">
                        <td class="p-1 text-right">{{post.id}}</td>
                        <td class="p-1 text-right">{{post.userId}}</td>
                        <td class="p-1">{{post.title}}</td>
                        <td class="p-1 text-md">{{post.body}}</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script setup>
    import {ref, reactive, onMounted} from 'vue';
    const posts = reactive([])

    onMounted(async () => {
        const resp = await fetch('https://jsonplaceholder.typicode.com/posts');
        posts.value = await resp.json()
    })
</script>