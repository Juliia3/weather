<script setup>
import { RouterLink, RouterView } from 'vue-router'
import './assets/styles/index.scss'
import Header from './components/Header/Header.vue'
</script>

<template>
  <Header />
  <header>

    <div class="wrapper">

      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav>
    </div>
  </header>

  <RouterView />
</template>
