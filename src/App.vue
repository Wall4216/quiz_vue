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
  let value = 0
  questions.value.map(q => {
    if (q.selected != null && q.answer == q.selected) {
      console.log('correct');
      value++
    }
  })
  return value
})
const getCurrentQuestion = computed(() => {
  let question = questions.value[currentQuestion.value]
  question.index = currentQuestion.value
  return question
})
const SetAnswer = (e) => {
  questions.value[currentQuestion.value].selected = e.target.value
  e.target.value = null
}
const NextQuestion = () => {
  if (currentQuestion.value < questions.value.length - 1) {
    currentQuestion.value++
    return
  }

  quizCompleted.value = true
}
</script>

<template>
  <main class="app">
    <h1>Тест</h1>
    <section class="quiz" v-if="!quizCompleted">
      <div class="quiz-info">
        <span class="question">{{ getCurrentQuestion.question }}</span>
        <span class="score">Score {{ score }}/{{ questions.length }}</span>
      </div>

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

      <button
          @click="NextQuestion"
          :disabled="!getCurrentQuestion.selected">
        {{
          getCurrentQuestion.index == questions.length - 1
              ? 'Finish'
              : getCurrentQuestion.selected == null
                  ? 'Select an option'
                  : 'Next question'
        }}
      </button>
    </section>

    <section v-else>
      <h2>You have finished the quiz!</h2>
      <p>Your score is {{ score }}/{{ questions.length }}</p>
    </section>
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
