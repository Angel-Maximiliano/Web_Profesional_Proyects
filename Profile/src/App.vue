<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>

      <nav>
        <ul>
          <li><RouterLink to="/">Home</RouterLink></li>
          <li><RouterLink to="/login">Login</RouterLink></li>
          <li><RouterLink to="/register">Register</RouterLink></li>
          <li><RouterLink to="/users">Users</RouterLink></li>
        </ul>
      </nav>

  </header>

  <RouterView />
</template>

<style scoped>

  nav{
    width: 100%;
    height: auto;
    background-color: rgba(111, 197, 157, 0.425);
  }

  nav ul {
    list-style-type: none;
    display: flex;
    justify-content: center;
  }

  nav ul li {
    font-size: 20px;
    margin: 0 1rem;
    text-align: center;
  }

  nav ul li a {
    display: block;
    color: white;
    text-align: center;
    padding: 14px 20px;
    text-decoration: none;
  }

  nav ul li a:hover {
    background-color: rgba(30, 44, 38, 0.582);
  }


</style>
