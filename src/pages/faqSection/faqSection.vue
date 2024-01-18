<script setup>
  import { ref, onMounted, onUnmounted } from 'vue';
  import faqItem from '../../components/faqItem/faqItem.vue';
  
  // FAQ's to populate the section with
  const faqs = ref([
  {
      index: 1,
      question: "What is Frontend Mentor, and how will it help me?",
      answer: "Frontend Mentor offers realistic coding challenges to help developers improve their frontend coding skills with projects in HTML, CSS, and JavaScript. It's suitable for all levels and ideal for portfolio building.",
  },
  {
      index: 2,
      question: "Is Frontend Mentor free?",
      answer: "Yes, Frontend Mentor offers both free and premium coding challenges, with the free option providing access to a range of projects suitable for all skill levels.",
  },
  {
      index: 3,
      question: "Can I use Frontend Mentor projects in my portfolio?",
      answer: "Yes, you can use projects completed on Frontend Mentor in your portfolio. It's an excellent way to showcase your skills to potential employers!",
  },
  {
      index: 4,
      question: "How can I get help if I'm stuck on a challenge?",
      answer: "The best place to get help is inside Frontend Mentor's Discord community. There's a help channel where you can ask questions and seek support from other community members.",
  }])

  // reference to keep track on which question to focus on when navigating using the arrow keys on the keyboard
  const focusedIndex = ref(-1);

  // Method to set focused on a FAQ item
  const setFocus = (index) => {
    const faqElements = document.querySelectorAll('.faqItem');
    if(faqElements[index]) {
      // Need to dig further into the selected object
      // to find the button, rather than the li to
      // set the focus on
      const faqButton = faqElements[index].querySelector('.accordionButton');
      if (faqButton) {
        faqButton.focus();
      }
      // If no button is found, focus the li
      else {
        faqElements[index].focus();
      }
      focusedIndex.value = index;
    }
  };
  

  // Method to handle arrow key navigation
  const handleKeydown = (event) => {
    if(event.key == "ArrowDown") {
      event.preventDefault();
      const nextIndex = (focusedIndex.value + 1) % faqs.value.length;
      setFocus(nextIndex);
    } else if (event.key == "ArrowUp") {
      event.preventDefault();
      const prevIndex = (focusedIndex.value - 1 + faqs.value.length) % faqs.value.length;
      setFocus(prevIndex);
    }
  };

  // The onMounted and onUnmounted adds and removes the
  // key press events when the objects get created and destroyed
  onMounted(() => {
    window.addEventListener('keydown', handleKeydown);
  });
  onUnmounted(() => {
    window.removeEventListener('keydown', handleKeydown);
  });

</script>

<template>
  <div>
    <div class="faqSection-header" id="faq-header">
      <img src="../../assets/images/icon-star.svg" alt="" aria-hidden="true">
      <h1>FAQs</h1>
    </div>
    <ul
      class="faqSection-list"
      aria-labelledby="faq-header"
      role="region"
      aria-live="polite"
      tabindex="0">
        <li
          v-for="(item, index) in faqs"
          class="faqItem"
          tabindex="-1">
            <faqItem
            :index="item.index"
            :title="item.question"
            :content="item.answer"
            @focus="focusedIndex = index"
            @blur="focusedIndex=-1" />
        </li>
    </ul>
  </div>
</template>

<style>

* {
  padding: 0px;
  margin: 0px;
}

.faqSection-header {
  display: flex;
  align-items: center;
  gap: 24px;
  height: 40px;
  padding: 53px 43px;
  padding-bottom: 12px;
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
  margin: 32px 40px;
  display: flex;
  flex-direction: column;
  gap: 19px;
}

.faqSection-list li {
  padding-bottom: 21px;
  border-bottom: 1px solid #0003;
}

.faqSection-list li:last-child {
  border-bottom: none;
  padding-bottom: 8px;
}
@media (max-width: 680px) {
  .faqSection-header {
    gap: 24px;
    padding: 0;
    margin: 24px 15px;
    margin-bottom: 14px;
    height: 40px;
  }
  .faqSection-header img {
    width: 22px;
  }
  .faqSection-header h1 {
    font-size: 34px;
  }
  .faqSection-list {
    margin: 20px;
    margin-top: 0;
  }
}


@media (max-width: 375px) {
  .faqSection-header {
    gap: 24px;
    padding: 0;
    margin: 24px 25px;
    margin-bottom: 18px;
    height: 40px;
  }
  .faqSection-header img {
    width: 22px;
  }
  .faqSection-header h1 {
    font-size: 34px;
  }
  .faqSection-list {
    margin: 23px;
    margin-top: 0;
  }
}

</style>