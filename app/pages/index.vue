<template>
    <div>
        <div class="text-3xl">@Home</div>
        <p class="text-lg my-8">
            A full-stack monorepo: <span class="font-bold">NuxtJs (Vue-3) frontend + Drogon C++ backend and SQLite3 database</span>, built for curiosity and performance.</p>

        <div class="flex flex-col gap-4 mb-8">
            <div class="text-2xl">Sample links</div>
            <ul class="flex flex-col gap-2 text-lg list-disc ml-8">
                <li><a class="font-bold text-blue-700" href="/posts">View Posts</a></li>
                <li><a class="font-bold text-blue-700" href="/categories">Categories (from Drogon API)</a></li>
                <li><a class="font-bold text-blue-700" href="/zone-times">Zone Times</a></li>
            </ul>
        </div>

        <div class="text-sm text-gray-600">
            <div class="my-4 text-2xl">Built by <span class="italic">Srikant Gudi, Bengaluru</span></div>
            <div class="my-4">(GitHub links)</div>
            <ul class="flex flex-col gap-2 text-lg list-disc ml-8">
                <li><a class="font-bold text-blue-700" href="https://github.com/srikantgudi/nuxapp" target="_blank">Nuxt app</a></li>
                <li><a class="font-bold text-blue-700" href="https://github.com/srikantgudi/drogsqliteapi" target="_blank">Drogon api</a></li>
            </ul>
        </div>
    </div>
</template>