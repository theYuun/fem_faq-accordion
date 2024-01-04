<template>
    <div class="bg_main">
        <div class="bg_top" >
            <img src="../../assets/images/bg-line.svg">
        </div>
    </div>
</template>

<script setup>

</script>

<style>
    .bg_main {
        position: absolute;
        top: 0;
        left: 0;
        width: 100vw;
        height: 100vh;
        aspect-ratio: 144.90;
        z-index: 0;
    }

    .bg_top {
        height: 320px;
        width: 100vw;
        background-color: #301334;
        display: flex;
        justify-content: flex-start;
    }

    .bg_top img {
        height: 100%;

    }
</style>