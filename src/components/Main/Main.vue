<script setup>
import './main.scss'
import Card from '../Card/Card.vue'
import cloud from '@/assets/img/cloudy.svg'
import bgCloud from '@/assets/img/bg_cloud.png'
import smallSun from '@/assets/img/small-sun.svg'
import axios from 'axios'

</script>

<template>
    <main class="main">
        <div class="main__container container">
            <div class="main__search dropdown">
                <input 
                class="main__input dropbtn" 
                type="search" 
                placeholder="Search..." 
                v-model="search"
                />
                <ul class="dropdown-content">
                    <li v-for="item in searchHandler" :key="item.id" @click="getApi(item.name)">
                        <p>{{ item.name }}</p>
                    </li>
                </ul>
            </div>
            <Card
            :day="today"
            :icon="cloud"
            :degrees="currentTemp+' °C'"
            :bg="bgCloud"
            :city="currentCity"
            time="13"
            :iconSmall="smallSun"
            degreesAll="25°C"
            />
        </div>
    </main>
</template>

<script>
import {cities} from '../data/cities'

export default {
    data() {
        return {
            currentCity: '',
            today: '',
            currentTemp: '',
            search: '',
            data: []
        }
    },
    created() {
        this.data = cities;
        this.getCityByIP();
        this.today = (new Date).toLocaleDateString("en-US", {weekday: 'long'});
    },
    computed: {
        searchHandler() {
            return this.data.filter(elem => {
                return this.search.length && elem.name.toLowerCase().includes(this.search.toLowerCase())
            })
        }
    },
    methods: {
        async getApi(city) {
            const getWeather = await axios.get(`https://api.openweathermap.org/data/2.5/weather?units=metric&q=${city.toLowerCase()}&appid=261514ec6ead072a338a344dce0fb58f`)
            
            const data = getWeather.data;
            this.search = city;
            this.currentCity = city;

            this.currentTemp = data.main.temp.toFixed(1)
            
            this.get7DaysForecast(data.coord.lat, data.coord.lon)
        },
        async get7DaysForecast(lat, lon) {
            const get7Days = await axios.get(`https://api.openweathermap.org/data/2.5/onecall?lat=${lat}&lon=${lon}&exclude=current,hourly,minutely,alerts&units=metric&appid=547343e58f273e78496cc775ed43bf31`)
            console.log(get7Days.data)
        },
        async getCityByIP() {
            const getCity = await axios.get('https://ipapi.co/json/');
            let data = getCity.data;
            this.getApi(data.city)
        },
    }
}

</script>