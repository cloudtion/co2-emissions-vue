<script setup lang="ts">
    import ParallaxImage from './ParallaxImage.vue';
    
    defineProps<{
        src: string,
        multiplier?: number,
    }>();
</script>

<template>
    <ParallaxImage src="bubble.svg"/>
</template>

<style>
    img{
        width: 100%;
        transform: translateY(5px);
    }
</style>