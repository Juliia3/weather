<script setup>
import './main.scss'
import Card from '../Card/Card.vue'
import cloud from '@/assets/img/cloudy.svg'
import bg_cloud from '@/assets/img/bg_cloud.png'
</script>

<template>
    <main class="main">
        <div class="main__container container">
            <div class="main__search">
                <input class="main__input" type="text" placeholder="Search..." />
            </div>
            <Card
            day="Friday"
            :icon="cloud"
            degrees="21°C"
            :bg="bg_cloud"
            />
        </div>
    </main>
</template>