<template>
    <div>
        <h2>Posts</h2>
        <div class="data-list-60">
            <table>
                <thead>
                    <tr>
                        <td>Title</td>
                        <td>Action</td>
                        <td>Body</td>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="p in data" :key="p.id">
                        <td width="30%">{{p.title}}</td>
                        <td width="10%">
                            [<router-link :to="`/post/${p.id}/comments`">Comments</router-link>]
                            [<router-link :to="`/post/${p.id}/info`">Info</router-link>]
                        </td>
                        <td>{{p.body}}</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<style>
    
    thead {
        position: sticky;
        top: 0;
        background-color: #666;
        color: whitesmoke;
    }
</style>

<script setup>
    const response = await fetch('https://jsonplaceholder.typicode.com/posts');
    const data = await response.json();
</script>