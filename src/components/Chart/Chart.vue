<script setup>
import './chart.scss'
import { Chart, registerables } from 'chart.js'
import { isProxy, toRaw } from 'vue';

const prop = defineProps({
    index:{
        type: Number
    },
    hours: {
        type: Array
    },
    temperatures: {
        type: Array
    }
});


</script>
<template>
        <div class="chart">
        <canvas :id="'chart' + index"></canvas>
    </div>
</template>

<script>
 
export default {
    name: 'Chart',
    created() {
    },
    watch:{
        hours: function(){
            this.renderChart();
            
        }
    },  
    data() {
        return {
            
        }
    },
    mounted() {
        this.renderChart();
        
    },
    methods:{
        renderChart(){
            let chartExist = Chart.getChart('chart'+this.index)
            if (chartExist){
                chartExist.destroy(); 
            }
            
            const ctx = document.getElementById('chart' + this.index);
            Chart.register(...registerables);
            new Chart(ctx, {
                type: 'bar',
                options: {
                    responsive: true,
                    plugins: {
                        legend: {
                            position: 'top',
                        },
                        title: {
                            display: false,
                            text: 'Chart.js Bar Chart'
                        }
                    }
                },
                data: {
                    labels: isProxy(this.hours) ? toRaw(this.hours): [],
                    datasets: [
                        {
                            label: "Temperature",
                            data: isProxy(this.temperatures) ? toRaw(this.temperatures) : [],
                            backgroundColor: "rgba(71, 183,132,.5)",
                            borderColor: "#47b784",
                            borderWidth: 3
                        }
                    ]
                },

            });
        }
    }
}
</script>



