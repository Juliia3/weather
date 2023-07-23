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
            <div class="card_bg"
            :style="{ 'background-image': 'url(' + bg + ')', display:'flex', justifyContent: 'center', alignItems: 'center', backgroundSize: 'cover', backgroundRepeat: 'no-repeat', width:'435px', height: '458px' }">
                <div class="card__title">
                    <div class="card__title-text">
                        <h1 class="card__day">{{ day }}</h1>
                        <div class="card__icon"><img :src="icon" alt="icon"></div>
                        <h2 class="card__degrees">{{ degrees }}</h2>
                    </div>
                </div>
            </div>
            <div class="card__info-block">
                <div class="card__filter">
                    <button class="card__button">Day</button>
                    <button class="card__button">Week</button>
                </div>
                <h2 class="card__city">{{ city }} <button class="plus">+</button></h2> 
                <div class="card__info">
                    <div class="card__info-box">
                        <p class="card__time">{{ time }}</p>
                        <div class="card__icon-small"><img :src="iconSmall" alt="icon"></div>
                        <p class="card__degrees">{{ degreesAll }}</p>
                    </div>
                    <div class="card__info-box">
                        <p class="card__time">{{ time }}</p>
                        <div class="card__icon-small"><img :src="iconSmall" alt="icon"></div>
                        <p class="card__degrees">{{ degreesAll }}</p>
                    </div>
                    <div class="card__info-box">
                        <p class="card__time">{{ time }}</p>
                        <div class="card__icon-small"><img :src="iconSmall" alt="icon"></div>
                        <p class="card__degrees">{{ degreesAll }}</p>
                    </div>
                    <div class="card__info-box">
                        <p class="card__time">{{ time }}</p>
                        <div class="card__icon-small"><img :src="iconSmall" alt="icon"></div>
                        <p class="card__degrees">{{ degreesAll }}</p>
                    </div>
                    <div class="card__info-box">
                        <p class="card__time">{{ time }}</p>
                        <div class="card__icon-small"><img :src="iconSmall" alt="icon"></div>
                        <p class="card__degrees">{{ degreesAll }}</p>
                    </div>
                    <div class="card__info-box">
                        <p class="card__time">{{ time }}</p>
                        <div class="card__icon-small"><img :src="iconSmall" alt="icon"></div>
                        <p class="card__degrees">{{ degreesAll }}</p>
                    </div>
                    <div class="card__info-box">
                        <p class="card__time">{{ time }}</p>
                        <div class="card__icon-small"><img :src="iconSmall" alt="icon"></div>
                        <p class="card__degrees">{{ degreesAll }}</p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>