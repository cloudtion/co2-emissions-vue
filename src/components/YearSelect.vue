<script setup lang="ts">
    import type { Ref } from "vue";
    import {ref} from "vue";

    const props = defineProps<{
        startYear : number,
        endYear : number 
    }>();

    const emit = defineEmits(['change']);

    const selectedYear : Ref<number> = ref(2019);
    
    const years : number[] = [];

    for(let y=props.endYear; y>=props.startYear; y--){

        years.push(y);
    }

    function selectedYearChanged(e : Event){
        
        const target = (<HTMLInputElement>e.target);
        const new_value = parseInt(target.value);

        selectedYear.value = new_value;
        emit("change", new_value);
    }
</script>

<template>

    <select @change="selectedYearChanged($event)" :value="selectedYear">
        <template v-for="year in years">
            <option :value="year">{{ year }}</option>
        </template>
    </select>

</template>

<style>
    #year-select-wrapper{
        text-align: center;
        margin-bottom: 1em;
    }

    #year-select-wrapper>select{
        font-size: 20px;
        padding: 0.25em 0.5em;
        border-radius: 5px;
    }
</style>