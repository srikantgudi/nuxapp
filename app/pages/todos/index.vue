<template>
    <div>
        <div class="text-3xl pb-2 border-b-2">Todos</div>
        <div class="shadow-lg shadow-gray-400" style="height:80vh;overflow-y: auto;">
            <table class="w-full">
                <thead class="bg-gray-800 text-gray-200 sticky top-0">
                    <tr>
                        <td class="p-1 w-15 text-right">Id</td>
                        <td class="p-1 w-20 text-right">User-Id</td>
                        <td class="p-1 w-auto">Title</td>
                        <td class="p-1 w-auto">Completed?</td>
                    </tr>
                </thead>
                <tbody>
                    <tr class="align-top even:bg-gray-200" v-for="todo in todos.value" :key="todo.id">
                        <td class="p-1 text-right">{{todo.id}}</td>
                        <td class="p-1 text-right">{{todo.userId}}</td>
                        <td class="p-1 text-lg">{{todo.title}}</td>
                        <td class="p-1 text-md">{{todo.completed}}</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script setup>
    import {ref, reactive, onMounted} from 'vue';
    const todos = reactive([])

    onMounted(async () => {
        const resp = await fetch('https://jsonplaceholder.typicode.com/todos');
        todos.value = await resp.json()
    })
</script>