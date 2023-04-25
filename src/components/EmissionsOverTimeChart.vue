<script setup lang="ts">
    import { onMounted, ref } from "vue";
    import Section from "@/components/Section.vue";
    import { Line } from "vue-chartjs";
    import { Chart as ChartJS, Title, Tooltip, Legend, LineElement, CategoryScale, PointElement, LinearScale, type LayoutPosition } from "chart.js";
    import CO2_OUTPUT_DATA from "@/assets/co2_output_data.csv";
    import {MONO_COLORS} from '@/ChartColors.js';

    ChartJS.register(Title, Tooltip, Legend, LineElement, CategoryScale, LinearScale, PointElement);

    const CHART_OPTIONS = {
        responsive: true,
        maintainAspectRatio: false,
        backgroundColor: 'white',
        color: '#2c5e3d',
        plugins: {
            
            legend: {
                position: ('bottom' as any),
                align: ('start' as any),
            }

        },
    };

    const chartData = ref({
        labels: [''],
        datasets: [
            {
                label: 'Data One',
                borderColor: '#f87979',
                data: [1]
            }
        ]
    }); 

    function createChartData(){

        const datasets : {label : string, borderColor : string, data : number[]}[] = [];   

        const START_YEAR = 1990;
        const END_YEAR = 2019;

        const column_labels : string[] = CO2_OUTPUT_DATA[0];
        const column_index_map : {[col_name:string] : number} = {};

        column_labels.forEach((col_name:string,ind:number)=>{

            column_index_map[col_name] = ind;
        })

        const col_index_2019 = column_index_map['2019'];
        const sorted_countries = CO2_OUTPUT_DATA.slice(1,CO2_OUTPUT_DATA.length-1).sort((a:any,b:any)=> parseInt(b[col_index_2019]) - parseInt(a[col_index_2019]));
        
        const top_10 = sorted_countries.slice(0, 10);
        
        top_10.forEach((row : any, ind:number) => {
            
            const country_emissions_data : number[] = [];

            for(let y=START_YEAR;y<=END_YEAR;y++){
                
                const parsed = parseInt(row[column_index_map[y]]);
                
                country_emissions_data.push(Number.isNaN(parsed)? 0 : parsed);
            }

            datasets.push({
                label: row[0],  // First column is country name.
                borderColor: MONO_COLORS[ind%MONO_COLORS.length],
                data: country_emissions_data,
            })
        });
        
        const year_labels : string[] = [];
        for(let y=START_YEAR; y<=END_YEAR; y++){

            year_labels.push(''+y);
        }

        chartData.value = {
            labels: year_labels,
            datasets
        };
    }

    onMounted(createChartData);
</script>

<template>
    <Section id='emissions-over-time' class='chart-wrapper'> 
        <Line
            :data="chartData" 
            :height="400"
            :options="CHART_OPTIONS"
        />
    </Section>
</template>