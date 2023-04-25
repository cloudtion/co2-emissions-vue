
<script setup lang="ts">
    defineProps<{
        index: number,
        countryName: string,
    }>();
</script>

<template>
    <div class="country-list-entry">
        <span class="country-name">{{index+1}}. {{countryName}}</span>
        <span><slot></slot></span>
    </div>
</template>