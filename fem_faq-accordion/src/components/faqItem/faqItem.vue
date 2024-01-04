<script setup>
import { ref, reactive } from 'vue'

const props = defineProps({
  title: {
    type: String,
    required: true
  },
  content: {
    type: String,
    required: true
  }
});

const toggleAnswerState = reactive({
  condition: false,
});

const isMouseOver = ref(false);

const toggleAnswer = () => {
  if(isMouseOver.value)
  {
    toggleAnswerState.condition = !toggleAnswerState.condition;
  }
  else
  {
    toggleAnswerState.condition = false;
  }
}

</script>

<template>
  <div class="accordionObject">
    <button
      class="accordionButton"
      @mouseover="isMouseOver = true"
      @mouseout="isMouseOver = false"
      @click="toggleAnswer">
        <div class="accordionButton-header">
          <div class="accordionButton-text" :class="{ 'accordionButton-text-open' : toggleAnswerState.condition }">
            {{ title }}
          </div>
          <div class="accordionButton-spacer"></div>
          <div class="accordionButton-icon" :class="{ 'accordionButton-icon-open' : toggleAnswerState.condition }">
            {{ toggleAnswerState.condition ? '-' : '+' }}
          </div>
        </div>
        <div class="accordionAnswer" :class="{ 'accordionAnswer-open' : toggleAnswerState.condition }">{{ content }}</div>
      </button>
  </div>
</template>

<style scoped>

  :root {
    --answerOpen: 0;
    --textColor: #2d0f31;
  }

  .accordionObject {
    margin: 2px 40px;
    padding: 0;
    border-bottom: 1px solid #0003;
  }
  
  .accordionButton {
    width: 100%;
    padding: 0;
    border-radius: 5px;
    background-color: #fff;
    border: none;
  }

  .accordionButton:hover {
    color: #af00eb;
  }

  .accordionButton:focus {
    outline-style: dashed 2px #af00eb;
    outline-offset: 3px 3px 0px 3px;
  }
  
  .accordionButton-header {
    display: flex;
    margin-top: 30px;
    flex-direction: row;
    align-items: center;
    border-radius: 0;
  }
  
  .accordionButton-text {
    text-align: left;
    font-size: 20px;
    letter-spacing: -1.05px;
    color: var(--textColor);
    font-weight: bold;
    transition: all 0.25s ease-out;
  }
  .accordionButton-text-open {
    --textColor: #af00eb;
    transition: all 0.25s ease-out;
  }
  .accordionButton-spacer {
    flex: 1;
  }
  .accordionButton-icon {
    width: 25px;
    height: 25px;
    background-color: #af00eb;
    border-radius: 50%;
    font-size: 20px;
    color: #fff;
    margin-top: 1px;
    margin-right: 3px;
    transition: all 0.25s ease-out;
  }
  .accordionButton-icon-open {
    background-color: #2d0f31;
    transition: all 0.25s ease-out;
  }
  
  .accordionAnswer {
    font-size: 16px;
    line-height: 24px;
    text-align: left;
    border-radius: 0px;
    padding: 15px 0px;
    color: #2d0f31;
    --answerOpen: 0;
    height: calc(91px * var(--answerOpen));
    transform-origin: 50% 0%;
    transform: scaleY(var(--answerOpen));
    transition: all 0.25s ease-out;
  }
  
  .accordionAnswer-open {
    --answerOpen: 1;
    --textColor: #af00eb;
    padding: 25px 0px;
    transition: all 0.25s ease-out;
  }

</style>
