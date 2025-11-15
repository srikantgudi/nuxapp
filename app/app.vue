<template>
  <header>
    <nav>
      <div id="app-title">NuxtJs Demo App</div>
      <div class="nav-links">
        <a href="/">Home</a>
        <a href="/posts">Posts</a>
        <a href="/comments">Comments</a>
        <a href="/zonetime">Zone-time</a>
        <a href="/calendar">Calendar</a>
        <a href="/about">About</a>
      </div>
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
  body {
    margin: 1vh 5vw;
  }
  #app-title {
    font-size: 3vw;
  }
  .nav-links {
    display: flex;
    font-size: large;
    gap: 1rem;
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
  @media screen and (max-width:640px) {
    td {padding:2%;}
    nav {
      display:flex;
      flex-wrap: wrap;
      font-size: 90%;
      margin:0;
    }
    #app-title {font-size: 3vw;}
    .nav-links {
      position: absolute;
      top:0;
      height: 24px;
      overflow-y: auto;
      right: 1rem;
      flex-direction: column;
      font-size: medium;
      gap: 1rem;
      color: #666;
    }
    .nav-links a {color:inherit;}
    .nav-links:hover {
      background-color: #999;
      padding: 0.5rem;
      z-index: 400;
      height: auto;
    }
    .nav-links:hover > a {
      color:whitesmoke;
    }
  }
</style>