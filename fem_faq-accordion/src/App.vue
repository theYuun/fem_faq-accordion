<script setup>
  import background from './components/Background/Background.vue';
  import faqSection from './pages/faqSection/faqSection.vue';
</script>

<template>
  <background class="bg" />
  <faqSection />
</template>

<style scoped>
  .bg {
    position: absolute;
    inset: 0;
  }
</style>
