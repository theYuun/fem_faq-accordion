<script setup>
  import { ref, reactive, defineProps, defineEmits } from 'vue';

  // The props sent from the faqSection
  const props = defineProps({
    index: {
      type: Number,
      required: true
    },
    title: {
      type: String,
      required: true
    },
    content: {
      type: String,
      required: true
    }
  })

  // The emits from the faqSection allows
  // the different faqItems to be focusable
  // independently
  const emit = defineEmits(['focus', 'blur']);

  // A boolean setting that is reactively togglable
  // and controls whether the answer for this faqItem
  // is expanded
  const toggleAnswerState = reactive({
    condition: false,
  });
  
  // Toggles the faqItems expanded boolean setting
  const toggleAnswer = () => {
    toggleAnswerState.condition = !toggleAnswerState.condition;
  }
  
  // Method to run the toggling function when
  // Enter of Space are pressed
  const handleKeypress = (event) => {
    if(event.key == "Enter" || event.key == " ") {
      event.preventDefault();
      toggleAnswer();
    }
  }

  const toggleIcon = toggleAnswerState.condition ? '../../assets/images/icon-minus.svg' : '../../assets/images/icon-plus.svg';

</script>
<template>
  <button
    class="accordionButton"
    @keydown="handleKeypress"
    @click="toggleAnswer"
    :aria-expanded="toggleAnswerState.condition.valueOf()"
    :aria-controls="'accordion-content-' + index"
    role="button">
      <div class="accordionButton-header">
        <div class="accordionButton-text" :class="{ 'accordionButton-text-open' : toggleAnswerState.condition }">
          {{ title }}
        </div>
        <div class="accordionButton-spacer"></div>
        <div class="accordionButton-icon" :class="{ 'accordionButton-icon-open' : toggleAnswerState.condition }"></div>
      </div>
    </button>
    <div
      :id="'accodion-content-' + index"
      class="accordionAnswer"
      :class="{ 'accordionAnswer-open' : toggleAnswerState.condition }"
      :aria-labelledby="'accordion-content-' + index"
      :aria-hidden="!toggleAnswerState.condition">
        {{ content }}
    </div>
</template>

<style scoped>

  :root {
    --answerOpenSize: 0;
    --headerTextColor: #2d0f31;
  }

  * {
    padding: 0;
    margin: 0;
    border: none;
    outline: none;
  }
  
  .accordionButton {
    width: 100%;
    padding: 5px 0px;
    border-radius: 5px;
    background-color: #fff;
    border: none;
  }

  .accordionButton:hover {
    color: #af00eb;
  }

  .accordionButton:focus {
    outline:solid 3px #af00eb;
    outline-offset: 5px;
  }
  
  .accordionButton-header {
    display: flex;
    flex-direction: row;
    align-items: center;
    border-radius: 0;
  }
  
  .accordionButton-text {
    text-align: left;
    font-size: 20px;
    letter-spacing: -1.05px;
    color: var(--headerTextColor);
    font-weight: bold;
    transition: all 0.25s ease-out;
  }
  .accordionButton-text-open {
    --headerTextColor: #af00eb;
    transition: all 0.25s ease-out;
  }
  .accordionButton-spacer {
    flex: 1;
  }
  .accordionButton-icon {
    position: relative;
    min-width: 30px;
    min-height: 30px;
    background: url('../../assets/images/icon-plus.svg');
    margin-top: 1px;
    margin-right: 3px;
    transition: all 0.25s ease-out;
  }
  .accordionButton-icon-open {
    background: url('../../assets/images/icon-minus.svg');
    transition: all 0.25s ease-out;
  }
  .accordionAnswer {
    font-size: 16px;
    line-height: 24px;
    text-align: left;
    border-radius: 0px;
    padding: 0px; /* padding is used to avoid unwanted space */
    color: #2d0f31;
    --answerOpenSize: 0;
    max-height: 0vh;
    opacity: 0;
    transform-origin: 50% 0%;
    transform: scaleY(var(--answerOpenSize));
    transition: all 0.25s ease-out;
  }
  
  .accordionAnswer-open {
    --answerOpenSize: 1;
    --headerTextColor: #af00eb;
    padding-top: 25px;
    max-height: 200px;
    opacity: 1;
    transition: all 0.25s ease-out;
  }

  @media (max-width: 375px) {
    
    .accordionButton-header {
    }
    .accordionButton {
      padding: 0;
      padding-top: 3px;
    }
    
    .accordionButton-text {
      font-size: 16px;
      width: 80%;
      letter-spacing: 0px;
      transition: all 0.25s ease-out;
    }

    .accordionButton-icon {
      margin-right: -1px;
    }

    .accordionAnswer {
      font-size: 14px;
      line-height: 21px;
    }
  }

</style>
