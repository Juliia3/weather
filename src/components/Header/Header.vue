<script setup>
import './header.scss'

</script>

<template>
    <header class="header">
        <div class="header__container container">
            <RouterLink to="/"><img class="logo" src="@/assets/img/logo.svg" alt="logo" /></RouterLink>
            <nav class="header__menu">
                <ul class="header__list">
                    <li class="header__item"><RouterLink class="header__link" to="/">Home</RouterLink></li>
                    <li class="header__item"><RouterLink class="header__link" to="/list">My List</RouterLink></li>
                </ul>
            </nav>
        </div>
    </header>
</template>