<script setup>
import { RouterLink, RouterView } from "vue-router";
import "./assets/styles/index.scss";
import Header from "./components/Header/Header.vue";
import Main from "./components/Main/Main.vue";
</script>

<template>
  <div class="page-wrapper">
    <Header />
    <Main />
    <RouterView />
  </div>
</template>
