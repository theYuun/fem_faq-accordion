<script setup>
  // very simply adding the background and content
  import background from './components/Background/Background.vue';
  import faqSection from './pages/faqSection/faqSection.vue';
</script>

<template>
  <background class="bg" />
  <faqSection class="content faqSection"/>
</template>

<style>
  .bg {
    position: absolute;
    inset: 0;
  }
  .content {
    position: relative;
    z-index: 2;
    margin-top: 96px;
  }
  
  .faqSection {
    display: flex;
    flex-flow: column;
    width: 80%;
    max-width: 600px;
    height: fit-content;
    background-color: #fff;
    box-shadow: 0 5px 10px -2px #0003;
    border-radius: 15px;
  }

  @media (max-width: 375px) {
    .faqSection {
      position: absolute;
      left: 24px;
      width: calc(100% - 48px);
      margin-top: 142px;
      border-radius: 10px;
    }
  }

  @media (max-width: 680px) {
    .faqSection {
      border-radius: 10px;
    }
  }
</style>
