<script setup>
import { RouterLink, RouterView } from "vue-router";
</script>

<template>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link
    href="https://fonts.googleapis.com/css2?family=Poppins&display=swap"
    rel="stylesheet"
  />
  <header>
    <div class="wrapper">
      <nav>
        <RouterLink to="/">{ Memory Game }</RouterLink>
        <RouterLink to="/about"></RouterLink>
      </nav>
    </div>
  </header>

  <RouterView />
</template>

<style>
* {
  margin: 0;
  padding: 0;
  font-family: "Poppins", sans-serif;
}
nav {
  display: flex;
  align-items: center;
  justify-content: space-around;
  background-color: #3498db;
  height: 50px;
}
nav a {
  text-decoration: none;
  color: white;
}
</style>
