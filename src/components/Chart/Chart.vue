<script setup>
import './chart.scss'
import { Chart, registerables } from 'chart.js'

defineProps({
    index:{
        type: Number
    }
});


</script>
<template>
        <div class="chart">
        <canvas :id="'chart'+index"></canvas>
    </div>
</template>

<script>
 
export default {
    name: 'Chart',
    data() {
        return {
            chartData: {
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
                    labels: ["10:00", "12:00", "14:00", "16:00", "18:00", "20:00", "22:00", "00:00"],
                    datasets: [
                        {
                            label: "Temperature",
                            data: [16, 20, 17, 25, 30, 20, 21, 22],
                            backgroundColor: "rgba(71, 183,132,.5)",
                            borderColor: "#47b784",
                            borderWidth: 3
                        }
                    ]
                },
 
            }
        }
    },
    mounted() {
        const ctx = document.getElementById('chart'+this.index);
        Chart.register(...registerables);
        new Chart(ctx, this.chartData);
 
    }
}
</script>



