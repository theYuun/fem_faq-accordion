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
        width: 100%;
        aspect-ratio: 144.90;
        z-index: 0;
    }

    .bg_top {
        height: 320px;
        width: 100%;
        background-color: var(--darkPurple);
        display: flex;
        justify-content: flex-start;
        overflow: hidden;
    }
    
    .bg_top img {
        height: 100%;
    }
    
    @media (max-width: 680px) {
        .bg_top {
            height: 232px;

        }

        .bg_top img {
            transform: translate(-460px, -40px);
            height: 300px;
        }
        
    }

</style>