<template>
    <div>
        <div class="text-3xl pb-2 border-b-2">Comments</div>
        <div class="shadow-lg shadow-gray-400" style="height:80vh;overflow-y: auto;">
            <table class="w-full">
                <thead class="bg-gray-800 text-gray-200 sticky top-0">
                    <tr>
                        <td class="p-1 w-10 text-right">Id</td>
                        <td class="p-1 w-20 text-right">Post-Id</td>
                        <td class="p-1 w-80">Name</td>
                        <td class="p-1 w-80">Email</td>
                        <td class="p-1 w-auto">Body</td>
                    </tr>
                </thead>
                <tbody>
                    <tr class="align-top even:bg-gray-200" v-for="post in posts.value" :key="post.id">
                        <td class="p-1 text-right">{{post.id}}</td>
                        <td class="p-1 text-right">{{post.postId}}</td>
                        <td class="p-1">{{post.name}}</td>
                        <td class="p-1">{{post.email}}</td>
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
        const resp = await fetch('https://jsonplaceholder.typicode.com/comments');
        posts.value = await resp.json()
    })
</script>