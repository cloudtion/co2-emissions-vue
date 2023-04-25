<script setup lang="ts">
    import ParallaxImage from '@/components/ParallaxImage.vue';
    import TopLeftImage from '@/assets/topleft.svg';
    import BubbleImage from '@/assets/bubble.svg';
</script>

<template>
    <ParallaxImage id="top-left-img" :src="TopLeftImage" :multiplier="0"/>

    <div>
        <ParallaxImage class="bubble-img" :src="BubbleImage" :multiplier="-0.3"/>
        <ParallaxImage class="bubble-img" :src="BubbleImage" :multiplier="-0.5"/>
        <ParallaxImage class="bubble-img" :src="BubbleImage" :multiplier="-0.7"/>

        <ParallaxImage class="bubble-img" :src="BubbleImage" :multiplier="-0.2"/>
        <ParallaxImage class="bubble-img" :src="BubbleImage" :multiplier="-0.4"/>
        <ParallaxImage class="bubble-img" :src="BubbleImage" :multiplier="-0.8"/>
        <ParallaxImage class="bubble-img" :src="BubbleImage" :multiplier="-0.7"/>
    </div>
</template>

<style>
    #top-left-img{
        position: absolute;
        top: 0;
        left: 0;
        width: 800px;
    }

    .bubble-img:nth-child(1){
        position: absolute;
        top: calc(120px + 90vh);
        width: 80px;
        left: 40px;
    }

    .bubble-img:nth-child(2){
        position: absolute;
        top: calc(50px + 90vh);
        width: 50px;
        left: 30px;
        transform: rotate(-78deg);
    }

    .bubble-img:nth-child(3){
        position: absolute;
        top: calc(0px + 90vh);
        width: 30px;
        left: 70px;
        transform: rotate(35deg);
    }

    .bubble-img:nth-child(4){
        position: absolute;
        top: calc(120px + 60vh);
        width: 60px;
        right: 40px;
    }

    .bubble-img:nth-child(5){
        position: absolute;
        top: calc(50px + 60vh);
        width: 75px;
        right: 110px;
        transform: rotate(-78deg);
    }

    .bubble-img:nth-child(6){
        position: absolute;
        top: calc(0px + 60vh);
        width: 42px;
        right: 70px;
        transform: rotate(35deg);
    }

    .bubble-img:nth-child(7){
        position: absolute;
        top: calc(-80px + 60vh);
        width: 30px;
        right: 90px;
        transform: rotate(35deg);
    }
</style>