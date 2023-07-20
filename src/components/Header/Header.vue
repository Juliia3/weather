<script setup>
import './header.scss'

</script>

<template>
    <header class="header">
        <div class="header__container container">
            <RouterLink to="/"><h1 class="header__logo logo">Weather</h1></RouterLink>
            <nav class="header__menu">
                <ul class="header__list">
                    <li class="header__item"><RouterLink class="header__link" to="/">Home</RouterLink></li>
                    <li class="header__item"><RouterLink class="header__link" to="/about">My List</RouterLink></li>
                </ul>
            </nav>
        </div>
    </header>
</template>