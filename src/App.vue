<script setup>

import {ref, computed, customRef} from "vue";

const questions = ref([
  {
    question: 'VUE JS',
    answer: 0,
    options: [
      'Верония это?',
      'web apps',
      'mobile apps',
    ],
    selected: null
  },
  {
    question: 'VUE JS',
    answer: 2,
    options: [
      'Это она',
      'web apps',
      'mobile apps',
    ],
    selected: null
  },
  {
    question: 'VUE JS',
    answer: 1,
    options: [
      'WTF',
      'web apps',
      'mobile apps',
      'quizzes'
    ],
    selected: null
  }
  ])

const quizCompleted = ref(false)
const currentQuestion = ref(0)
const score = computed(() => {
  let value = 0;
  questions.value.map(q => {
    if (q.selected == q.answer)
    {
      value++;
    }
  })
  return value
})

const getCurrentQuestion = computed(() => {
  let question = questions.value[currentQuestion.value]
  question.index = currentQuestion.value
  return question
})

const SetAnswer = e => {
  questions.value[currentQuestion.value].selected = e.target.value
  evt.target.value = null
}

const NextQuestion = () => {
  if (currentQuestion.value == questions.value.length -1)
  {
    currentQuestion.value++
  }
  else {
    currentQuestion.value--
  }
}
</script>

<template>
  <main class="app">
    <h1>Тест</h1>
    <section class="section">
      <span class="question">{{ getCurrentQuestion.question }}</span>
      <span class="score">Score {{score}} / {{questions.length}}</span>
    </section>
    <div class="options">
      <label
          v-for="(option, index) in getCurrentQuestion.options"
          :for="'option' + index"
          :class="`option ${
						getCurrentQuestion.selected == index
							? index == getCurrentQuestion.answer
								? 'correct'
								: 'wrong'
							: ''
					} ${
						getCurrentQuestion.selected != null &&
						index != getCurrentQuestion.selected
							? 'disabled'
							: ''
					}`">
        <input
            type="radio"
            :id="'option' + index"
            :name="getCurrentQuestion.index"
            :value="index"
            v-model="getCurrentQuestion.selected"
            :disabled="getCurrentQuestion.selected"
            @change="SetAnswer"
        />
        <span>{{ option }}</span>
      </label>
    </div>
  </main>
</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Montserrat', sans-serif ;

}

body {
  background-color:  black;
  color: white;
}
</style>
