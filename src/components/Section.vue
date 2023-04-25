<script setup lang="ts">
    const props = defineProps<{
        id? : string,
        class? : string
    }>();
</script>

<template>
    <div :id="id" :class="'section '+props.class">
        <slot></slot>
    </div>
</template>

<style>
    .section{
        margin: auto;
        display: flex;
        width: 1000px;
        max-width: 90vw;
        margin: auto;
        margin-bottom: 2em;
        position: relative;
    }
</style>