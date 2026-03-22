<script setup lang="ts">
import "./app.css"
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>
    <div class="wrapper">
      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
        <RouterLink to="/create">Create</RouterLink>
      </nav>
    </div>
  </header>

  <RouterView />
</template>

