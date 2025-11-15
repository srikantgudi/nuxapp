<template>
  <header>
    <nav>
      <h1>NuxtJs Demo App</h1>
      <a href="/">Home</a>
      <a href="/posts">Posts</a>
      <a href="/comments">Comments</a>
      <a href="/zonetime">Zone-time</a>
      <a href="/calendar">Calendar</a>
      <a href="/about">About</a>
    </nav>
  </header>
  <main>
    <NuxtPage />
  </main>
</template>

<style>
  * {
    font-family: helvetica;
  }
  nav {
    display: flex;
    align-items: center;
    gap: 1rem;
  }
  a {
    box-sizing: border-box;
    text-decoration: none;
    font-weight: 500;
    color: navy;
  }
  a:hover {
    color:blue;
  }
  .data-list {
    height: 70vh;
    overflow-y: auto;
  }
  .data-list-60 {
    height: 60vh;
    overflow-y: auto;
  }
  thead {
    background-color: #666;
    color: whitesmoke;
    position: sticky;
    top: 0;
  }
  td {
    padding: 0.25rem 0.5rem;
  }
  tbody tr:nth-child(even) {
    background-color: #e9e9e9;
  }
  table {
    box-shadow: 1px 2px 12px #999;
  }
  .para-title {
    font-size: 1.4rem;
    font-weight: 500;
  }
  .dflex {
    display: flex;
    align-items: center;
    gap: 1rem;
  }
  .vflex {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    gap: 1rem
  }
  .mt-10 {
    margin-top: 1rem;
  }
  .hand {
    transition: all 0.5s;
  }
  .mr-sm {
    margin-right: 1rem;
  }
  .mr-md {
    margin-right: 1.5rem;
  }
  .align-center {
    align-items: center;
  }
</style>