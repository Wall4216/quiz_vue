<script setup>

import {ref, computed} from "vue";

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

</script>

<template>
  <h1>hello world</h1>
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
