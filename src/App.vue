<script setup>
import { RouterLink, RouterView } from 'vue-router'
import './assets/styles/index.scss'
import Header from './components/Header/Header.vue'
import Main from './components/Main/Main.vue'
</script>

<template>
  <div class="page-wrapper">
      <Header />
      <Main />
  <!-- <header>

    <div class="wrapper">

      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav>
    </div>
  </header> -->

  <!-- <RouterView /> -->
  </div>

</template>
