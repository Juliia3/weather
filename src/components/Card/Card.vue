<script setup>
import './card.scss'

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

})
</script>

<template>
    <div class="card">
        <div class="card__container">
            <div class="card__title">
                <img class="card__bg" :src="bg">
                <div class="card__title-text">
                   <h1 class="card__day">{{ day }}</h1>
                    <div class="card__icon"><img :src="icon" alt="icon"></div>
                    <h2 class="card__degrees">{{ degrees }}</h2> 
                </div>
                
            </div>
        </div>
    </div>
</template>