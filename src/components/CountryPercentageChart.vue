<script setup lang="ts">

    import { onMounted, reactive, ref, type Ref } from "vue";
    import Section from "@/components/Section.vue";
    import { Doughnut } from "vue-chartjs";
    import { Chart as ChartJS, Title, Tooltip, Legend, ArcElement, CategoryScale, LinearScale } from "chart.js";
    import CO2_OUTPUT_DATA from "@/assets/co2_output_data.csv";
    import CountryListEntry from "@/components/CountryListEntry.vue";
    import {MONO_COLORS} from "@/ChartColors.js";
    import YearSelect from "@/components/YearSelect.vue";
    import type {CountryYearEmissions} from '@/types';
    
    ChartJS.register(Title, Tooltip, Legend, ArcElement, CategoryScale, LinearScale);

    const state = reactive({
        currentYear: 2019,
        chartData: {
            labels: [''],
            datasets: [ { data: [0], backgroundColor: ['gray']} ]
        },
        chartOptions: {
            responsive: true,
            borderColor: '#4c875f',
            plugins: {
                legend: {
                    display: false,
                },
            },
        },
    });

    const allCountriesData : Ref<CountryYearEmissions[]> = ref([]);

    function createChartData(){
        
        const column_labels : string[] = CO2_OUTPUT_DATA[0];
        const year_label_index : number = column_labels.indexOf(''+state.currentYear);

        const new_labels : string[] = [];
        const new_values : number[] = [];
        const new_colors : string[] = [];

        const countries_data : CountryYearEmissions[] = [];
        
        CO2_OUTPUT_DATA
            .slice(1, CO2_OUTPUT_DATA.length-1)
            .map((row:string[]) => ({
                country_name : row[0],
                year_emissions_value: parseInt(row[year_label_index])
            }))
            .sort((a:CountryYearEmissions, b:CountryYearEmissions)=> b.year_emissions_value-a.year_emissions_value)
            .forEach((entry:CountryYearEmissions) => {
                countries_data.push(entry);
            });
        
        
        allCountriesData.value = [...countries_data];

        const top_20_countries_data : CountryYearEmissions[] = countries_data.slice(0, 20);

        top_20_countries_data.forEach((entry:CountryYearEmissions, ind:number)=>{
            
            new_labels.push(entry.country_name);
            new_values.push(entry.year_emissions_value);
            new_colors.push(MONO_COLORS[ind%MONO_COLORS.length]);
        });

        const other_countries_emission_total : number = countries_data.slice(20, countries_data.length-20).reduce((total, entry:CountryYearEmissions)=> total+entry.year_emissions_value, 0);

        new_labels.push('Rest of the World');
        new_values.push(other_countries_emission_total);
        new_colors.push('lightgray');

        state.chartData = {
            labels: new_labels,
            datasets: [
                {   
                    backgroundColor: new_colors,
                    data: new_values
                }
            ]
        };
    }

    onMounted(createChartData);

    const num_format = new Intl.NumberFormat();

</script>


<template>

    <Section id="country-breakdown-wrapper">
        <div className='chart-wrapper'>
            
            <h2>{{state.currentYear}} CO<sub>2</sub> emissions By Country (kt)</h2>
                
            <Doughnut 
                :height="400"
                :width="400"
                :options="state.chartOptions"
                :data="state.chartData"
            />
    
        </div>

        <div>
            <div id="year-select-wrapper">
                <YearSelect 
                    @change="(new_year) =>{ state.currentYear = new_year; createChartData()}" 
                    :startYear="2000" 
                    :endYear="2019"
                />
            </div>

            <div id="country-list-wrapper">

                <div class="country-list">
                    <template v-for="entry, index in allCountriesData">
                        <CountryListEntry :index="index" :countryName="entry.country_name">
                            {{num_format.format(entry.year_emissions_value)}} kt
                        </CountryListEntry>
                    </template>
                </div>

            </div>
        </div>

    </Section>

</template>


<style>

    #country-list-wrapper{
        height: 400px;
        overflow: hidden;
        background: white;
        border-radius: 10px;
    }

    .country-list{
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        justify-content: space-between;
        height: 100%;
        overflow-y: auto;
    }

    .country-list-entry{
        width: 100%;
        display: inline-flex;
        align-items: center;
        flex-direction: row;
        justify-content: space-between;
        padding: 5px 10px;
    }

    .country-name{
        flex-grow: 1;
    }

    .country-bullet{
        width: 0.8em;
        height: 0.8em;
        border-radius: 50%;
        margin-right: 0.5em;
    }

    #country-breakdown-wrapper{
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
        align-items: flex-end;
        justify-content: space-evenly;
        margin-top: 2em;
    }

    #country-breakdown-wrapper>div{
        margin-bottom: 2em;
    }
</style>