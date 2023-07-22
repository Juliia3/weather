<script setup>
import './main.scss'
import Card from '../Card/Card.vue'
import cloud from '@/assets/img/cloudy.svg'
import bgCloud from '@/assets/img/bg_cloud.png'
import smallSun from '@/assets/img/small-sun.svg'
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
            :bg="bgCloud"
            city="London"
            time="13"
            :iconSmall="smallSun"
            degreesAll="25°C"
            />
        </div>
    </main>
</template>