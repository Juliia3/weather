<script setup>
import axios from 'axios'
defineProps({
    getCurrentWeather:{
        type: Function
    }
});

</script>

<template>
    <div class="dropdown">
        <input class="main__input dropbtn" type="search" placeholder="Search..." v-model="search"
        @keypress="getCitiesList" />
        <ul class="dropdown-content">
            <li v-for="item in data" @click="getCurrentWeather(item.name)">
                <p>{{ item.name }}, {{ item.country }}</p>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    data() {
        return {
            search: '',
            data: [],
            citiesApiConfig: {
                headers: {
                    "X-Api-Key": "9omKBDiU5H2/HfwN1VKzng==hG2jtO3UCRA9UvPq"
                }
            },
        }
    },
    methods:{
        searchFunc(){
            this.onsearch(this.search);
        },
        async getCitiesList() {
            if (!this.search.length) {
                this.data = [];
                return;
            }
            const citiesList = await axios.get(`https://api.api-ninjas.com/v1/city?name=${this.search.toLowerCase()}&limit=10&min_population=40000`, this.citiesApiConfig)
            this.data = citiesList.data
        },
    }
}
</script>