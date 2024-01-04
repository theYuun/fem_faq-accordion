<script setup>
    import { ref } from 'vue';
    import faqItem from '../../components/faqItem/faqItem.vue';

    const faqs = ref([
    {
        question: "What is Frontend Mentor, and how will it help me?",
        answer: "Frontend Mentor offers realistic coding challenges to help developers improve their frontend coding skills with projects in HTML, CSS, and JavaScript. It's suitable for all levels and ideal for portfolio building.",
    },
    {
        question: "Is Frontend Mentor free?",
        answer: "Yes, Frontend Mentor offers both free and premium coding challenges, with the free option providing access to a range of projects suitable for all skill levels.",
    },
    {
        question: "Can I use Frontend Mentor projects in my portfolio?",
        answer: "Yes, you can use projects completed on Frontend Mentor in your portfolio. It's an excellent way to showcase your skills to potential employers!",
    },
    {
        question: "How can I get help if I'm stuck on a challenge?",
        answer: "The best place to get help is inside Frontend Mentor's Discord community. There's a help channel where you can ask questions and seek support from other community members.",
    }])
</script>

<template>
  <div class="faqSection">
    <div class="faqSection-header">
      <img src="../../assets/images/icon-star.svg">
      <h1>FAQs</h1>
    </div>
        <ul class="faqSection-list">
            <li v-for="item in faqs" class="faqItem">
                <faqItem
                :title="item.question"
                :content="item.answer" />
            </li>
        </ul>
  </div>
</template>

<style scoped>

.faqSection {
  position: relative;
  z-index: 2;
  width: 600px;
  height: fit-content;
  margin-top: 136px;
  background-color: #fff;
  box-shadow: 0 5px 10px -2px #0003;
  border-radius: 15px;
  display: flex;
  flex-flow: column;
}

.faqSection-header {
  display: flex;
  align-items: center;
  gap: 24px;
  height: 40px;
  padding: 53px 43px;
  padding-bottom: 15px;
  letter-spacing: -1.5px;
}

.faqSection-header img {
  width: 36px;
}
.faqSection-header h1 {
  font-size: 58px;
}

.faqSection-list {
  list-style-type: none;
  padding: 0;
  margin: 0;
}

.faqSection-list li {
  width: 100%;
}
/*

@media (max-width: 600px) {
  .faqSection {
    width: 330px;
    margin-top: 110px;
  }
}
*/
</style>