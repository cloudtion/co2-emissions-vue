
<script setup lang="ts">
    import { reactive, onMounted, onBeforeUnmount } from "vue";

    const props = defineProps<{
        src : string,
        class? : string
        multiplier? : number,
    }>();

    const styleObject = reactive({
        transform: "translateY(0px)",
    });

    const onScroll = ()=>{
        styleObject.transform = `translateY(${window.pageYOffset*(props.multiplier?? 0.3)}px)`;
    }

    onMounted(()=>{

        window.addEventListener('scroll', onScroll);
    });

    onBeforeUnmount(()=>{

        window.removeEventListener("scroll", onScroll);
    });
</script>

<template>
    <img class="parallax-img" :src="src" :style="styleObject" :class="class" draggable="false" />
</template>

<style>
.parallax-img{
    opacity: 0.2;
}
</style>