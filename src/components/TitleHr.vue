<script setup lang="ts">
    defineProps<{
        sideLineHeight? : number,
    }>();
</script>

<template>
    <div class="title-hr">
        <div class="title-hr-line" :style="{ height: (sideLineHeight?? 1)+'px' }"></div>
        <slot></slot>
        <div class="title-hr-line" :style="{ height: (sideLineHeight?? 1)+'px' }"></div>
    </div>
</template>

<style>
    .title-hr{
        display: flex;
        flex-direction: row;
        align-items: center;
        width: 100%;
    }

    .title-hr-line{
        flex-grow: 1;
        height: 4px;
        width: 10px;
        background-color: currentColor;
        margin: 0 1em;
        border-radius: 5px;
    }
</style>