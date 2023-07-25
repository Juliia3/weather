<script setup>
import './main.scss'
import Card from '../Card/Card.vue'

import cloud from '@/assets/img/cloud.svg'
import bgCloud from '@/assets/img/bg-cloud.png'

import sun from '@/assets/img/sun.svg'
import bgSun from '@/assets/img/bg-sun.png'

import rain from '@/assets/img/rain.svg'
import bgRain from '@/assets/img/bg-rain.png'

import thunder from '@/assets/img/thunder.svg'
import bgThunder from '@/assets/img/bg-thunder.png'

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
                @keypress="getCitiesList()"
                @search="getCitiesList()"
                />
                <ul class="dropdown-content">
                    <!-- <li v-for="item in searchHandler" :key="item.id" @click="getApi(item.name)">
                        <p>{{ item.name }}</p>
                    </li> -->
                    <li v-for="item in data" @click="getCurrentWeather(item.name)">
                        <p>{{ item.name }}, {{ item.country }}</p>
                    </li>
                </ul>
            </div>
            <Card
            :day="today"
            :icon="getWeatherIcon()"
            :degrees="currentTemp+' °C'"
            :bg="bgSun" 
            :city="currentCity"
            time="13"
            :iconSmall="smallSun"
            degreesAll="25°C"
            />
        </div>
    </main>
</template>

<script>
// import {cities} from '../data/cities'
// import { getCurrentInstance } from 'vue'

export default {
    data() {
        return {
            currentCity: '',
            today: '',
            currentTemp: '',
            search: '',
            data: [],
            citiesApiConfig: {
                headers: {
                    "X-Api-Key": "9omKBDiU5H2/HfwN1VKzng==hG2jtO3UCRA9UvPq"
                }
            },
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
        // this.data = cities;
        this.getCityByIP();
        this.today = (new Date).toLocaleDateString("en-US", {weekday: 'long'});
    },
    // computed: {
    //     async searchHandler() {
    //         if (this.search.length){
    //             const cities = await this.getCitiesList(this.search)
    //             console.log(cities)
    //             return cities;
    //     }
    //     return []
    // }
    // },
    methods: {
        async getCurrentWeather(city) {
            const getWeather = await axios.get(`https://api.openweathermap.org/data/2.5/weather?units=metric&q=${city.toLowerCase()}&appid=261514ec6ead072a338a344dce0fb58f`)
            
            const data = getWeather.data;
            this.search = city;
            this.currentCity = city;

            this.currentTemp = data.main.temp.toFixed(1)
            
            this.get7DaysForecast(data.coord.lat, data.coord.lon)
        },
        async get7DaysForecast(lat, lon) {
            const get7Days = await axios.get(`https://api.openweathermap.org/data/2.5/onecall?lat=${lat}&lon=${lon}&exclude=current,hourly,minutely,alerts&units=metric&appid=547343e58f273e78496cc775ed43bf31`)
            // console.log(get7Days.data)
        },
        async getCityByIP() {
            const getCity = await axios.get('https://ipapi.co/json/');
            let data = getCity.data;
            // this.getApi(data.city)
            this.getCurrentWeather(data.city)
        },
        // async getCitiesList(search) {
        //     const config = {
        //         headers: {
        //             "X-Api-Key": "9omKBDiU5H2/HfwN1VKzng==hG2jtO3UCRA9UvPq"
        //         }
        //     };
        //     const citiesList = await axios.get(`https://api.api-ninjas.com/v1/city?name=${search.toLowerCase()}&limit=10`, config)
        //     return citiesList.data
        // }
        async getCitiesList() { 
            if (!this.search.length){
                this.data = [];
                return;
            }
            const citiesList = await axios.get(`https://api.api-ninjas.com/v1/city?name=${this.search.toLowerCase()}&limit=10&min_population=40000`, this.citiesApiConfig)
            this.data = citiesList.data
    },
    getWeatherIcon() {
        if (
            !this.currentCity.data || 
            !this.currentCity.data.weather || 
            (this.data.weather[0].id >= 700 && this.currentCity.data.weather[0] < 800) ||
            !this.weatherIcons[this.currentCity.data.weather[0].main] 
            ) {
               return this.weatherIcons["Clouds"]; 
            }
            else if (
            !this.currentCity.data || 
            !this.currentCity.data.weather || 
            (this.data.weather[0].id >= 200 && this.currentCity.data.weather[0] < 233) ||
            !this.weatherIcons[this.currentCity.data.weather[0].main] 
            ) {
               return this.weatherIcons["Thunderstorm"]; 
            }
            else if (
            !this.currentCity.data || 
            !this.currentCity.data.weather || 
            (this.data.weather[0].id >= 300 && this.currentCity.data.weather[0] < 532) ||
            !this.weatherIcons[this.currentCity.data.weather[0].main] 
            ) {
               return this.weatherIcons["Rain"]; 
            }
            else if (
            !this.currentCity.data || 
            !this.currentCity.data.weather || 
            (this.data.weather[0].id >= 800 && this.currentCity.data.weather[0] < 801) ||
            !this.weatherIcons[this.currentCity.data.weather[0].main] 
            ) {
               return this.weatherIcons["Clear"]; 
            }
            return this.weatherIcons[this.currentCity.data.weather[0].main]
    }
}
}

</script>