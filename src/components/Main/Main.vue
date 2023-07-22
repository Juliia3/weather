<script setup>
import './main.scss'
import Card from '../Card/Card.vue'
</script>

<template>
    <main class="main">
        <div class="main__container container">
            <div class="main__search">
                <input class="main__input" type="text" placeholder="Search..." />
            </div>
            <Card
            day="Friday"
            icon="../../assets/img/cloudy.png"
            />
        </div>
    </main>
</template>