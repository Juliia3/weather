<script setup>
import './block.scss'
import Card from '../Card/Card.vue'

import Search from '../Search/Search.vue'

import cloud from '@/assets/img/cloud.svg'
import bgCloud from '@/assets/img/bg-cloud.png'

import sun from '@/assets/img/sun.svg'
import bgSun from '@/assets/img/bg-sun.png'

import rain from '@/assets/img/rain.svg'
import bgRain from '@/assets/img/bg-rain.png'

import thunder from '@/assets/img/thunder.svg'
import bgThunder from '@/assets/img/bg-thunder.png'

import axios from 'axios'


const prop = defineProps({
    index:{
        type: Number
    },
    add:{
        type: Function
    }
});



</script>

<template>
    <div class="block__container container">
            <div class="search-row">
                <Search :getCurrentWeather="getCurrentWeather"></Search>
                <button @click="add" class="plus">+</button>
            </div>
            
            <Card :index="index" :day="today" :icon="getWeatherIcon()['main']" :degrees="currentTemp + ' °C'" :bg="getWeatherIcon()['bg']"
                :city="currentCity.name ? currentCity.name : ''" :hours="hours" :temperatures="temperatures" />
    </div>
</template>

<script>
export default {
    data() {
        return {
            currentCity: '',
            hours:[],
            temperatures:[], 
            today: '',
            currentTemp: '',
            search: '',
            weatherIcons: {
                Clouds: {
                    main: cloud,
                    bg: bgCloud,
                },
                Clear: {
                    main: sun,
                    bg: bgSun,
                },
                Rain: {
                    main: rain,
                    bg: bgRain,
                },
                ThunderStorm: {
                    main: thunder,
                    bg: bgThunder,
                },

            }
        }
    },
    created() {
        this.getCityByIP();
        this.today = (new Date).toLocaleDateString("en-US", { weekday: 'long' });
    },
    methods: {
        async getCurrentWeather(city) {
            const getWeather = await axios.get(`https://api.openweathermap.org/data/2.5/weather?units=metric&q=${city.toLowerCase()}&appid=261514ec6ead072a338a344dce0fb58f`)

            const data = getWeather.data;
            this.search = city;
            this.currentCity = {
                name: city,
                data: data
            };

            this.currentTemp = data.main.temp.toFixed(1)

            this.getHourlyForecast(data.coord.lat, data.coord.lon)
        },
        async getHourlyForecast(lat, lon) {
            const forecast = await axios.get(`https://api.openweathermap.org/data/2.5/forecast?lat=${lat}&lon=${lon}&exclude=current,minutely,alerts&cnt=10&units=metric&appid=547343e58f273e78496cc775ed43bf31`)
            let temperatures = []
            let hours = [];
            forecast.data.list.forEach(function(e){
                let hour = e.dt_txt.split(" ")[1]
                hours.push(hour.substr(0,5))
                temperatures.push(e.main.temp)
            })
            this.hours = hours;
            this.temperatures = temperatures;
        },
        async getCityByIP() {
            const getCity = await axios.get('https://ipapi.co/json/');
            let data = getCity.data;
            // this.getApi(data.city)
            this.getCurrentWeather(data.city)
        },
       
        getWeatherIcon() {
            if (
                !this.currentCity.data ||
                !this.currentCity.data.weather ||
                (this.currentCity.data.weather[0].id >= 700 && this.currentCity.data.weather[0].id < 800) ||
                !this.weatherIcons[this.currentCity.data.weather[0].main]
            ) {
                return this.weatherIcons["Clouds"];
            }
            return this.weatherIcons[this.currentCity.data.weather[0].main]
        }
    }
}

</script>