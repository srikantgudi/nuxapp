<script setup>
import { ref, onMounted } from 'vue'
import { useRoute } from 'vue-router'

defineProps({
    comments: {
        type: Array,
        required: true
    }
})
</script>

<template>
    <div class="data-list-60">
        <table>
            <thead>
                <tr>
                    <td align="right">Id</td>
                    <td>Name</td>
                    <td>Email</td>
                    <td>Body</td>
                </tr>
            </thead>
            <tbody>
                <tr v-for="c in comments" :key="c.id">
                    <td align="right">{{c.id}}</td>
                    <td>{{c.name}}</td>
                    <td>{{c.email}}</td>
                    <td>{{c.body}}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>