<script setup>
import './card.scss'
import Chart from '../Chart/Chart.vue'

defineProps({
    city: {
        type: String,
        required: true
    },
    degrees: {
        type: Number,
        required: true
    },
    icon: {
        type: String,
        required: true
    },
    bg: {
        type: String,
        required: true
    },
    day: {
        type: String,
        required: true
    },
    time: {
        type: String,
        required: true
    },
    iconSmall:{
        type: String,
        required: true
    },
    degreesAll: {
        type: Number,
        required: true
    },
})
</script>

<template>
    <div class="card">
        <div class="card__container">
            <div class="card__bg">
                <img class="card__bg-img" :src="bg" alt="bg">
                <div class="card__title-text">
                    <h1 class="card__day">{{ day }}</h1>
                    <div class="card__icon"><img :src="icon" alt="icon"></div>
                    <h2 class="card__degrees">{{ degrees }}</h2>
                </div>
            </div>
            <div class="card__info-block">
                <div class="card__filter">
                    <button class="card__button">Day</button>
                    <button class="card__button">Week</button>
                </div>
                <h2 class="card__city">{{ city }} <button class="plus">+</button></h2> 
                <div class="card__info">
                    <Chart />
                </div>
            </div>
        </div>
    </div>
</template>