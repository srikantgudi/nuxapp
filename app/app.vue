<template>
  <div class="w-4/5 m-auto">
    <nav class="flex items-center gap-2 my-4 border-b pb-4 border-gray-400">
      <div class="text-4xl mr-12">Nuxt Demo App</div>
      <NuxtLink class="font-bold" to="/">Home</NuxtLink>
      <span class="text-blue-700">External APIs &raquo;</span>
      <NuxtLink class="font-bold" to="/posts">Posts</NuxtLink>
      <NuxtLink class="font-bold" to="/comments">Comments</NuxtLink>
      <NuxtLink class="font-bold" to="/todos">ToDos</NuxtLink>
      <span class="text-blue-700">Drogon APIs &raquo;</span>
      <NuxtLink class="font-bold" to="/categories">Categories</NuxtLink>
      <NuxtLink class="font-bold" to="/products">Products</NuxtLink>
      <NuxtLink class="font-bold" to="/customers">Customers</NuxtLink>
      <span class="text-blue-700">Misc. &raquo;</span>
      <NuxtLink class="font-bold" to="/zonetimes">Zone-times</NuxtLink>
    </nav>
    <NuxtPage/>
  </div>
</template>
