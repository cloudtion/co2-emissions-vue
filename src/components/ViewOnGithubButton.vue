<script setup lang="ts">
    import GithubLogo from "@/assets/github-mark.svg";
</script>

<template>
    <a class="view-on-github" href="https://github.com/cloudtion/co2-emissions-vue">
        <div>
            <img class="github-logo" alt="Github Logo" :src="GithubLogo"/>
        </div>
        <span>View on Github</span>
    </a>
</template>

<style>
.view-on-github{
    position: absolute;
    top: 1em;
    right: 1em;
    background: -webkit-gradient(linear,left top,left bottom,color-stop(0,#eee),to(#ddd));
    background: linear-gradient(to bottom,#eee 0,#ddd 100%);
    border-radius: 4px;
    border: 1px solid black;
    color: black;
    text-decoration: none;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    padding: 5px 10px;
}
.view-on-github>span{
    margin-left: 5px;
}

.github-logo{
    width: 20px;
}
</style>