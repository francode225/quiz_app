<template>
  <div>
    <div class="wrapper">
      <form @submit.prevent="submitReponses" v-if="!montrerScore">
        <div class="q">{{ compteurQuestion + 1 }}- {{ selectedQuestion.question }}</div>
        <div class="question">
          <div v-for="(answer, index) in selectedQuestion.answers" :key="index" class="option">
            <input
              type="radio"
              :id="`option${index}`"
              :name="answer"
              :value="answer"
              v-model="reponse"
            />
            <label :for="`option${index}`">{{ answer }}</label>
          </div>
        </div>

        <button type="submit">Submit</button>
      </form>
      <div v-else class="score">
        <h3>
          {{ message }} votre score est de <span>{{ score }}/50</span>
        </h3>
      </div>
    </div>
  </div>
</template>

<style scoped>
.wrapper {
  height: 300px;
  width: 400px;
  background-color: #fff;
  border-radius: 10px;
}

form {
  height: 100%;
  display: flex;
  flex-direction: column;
}

.question {
  flex: 1;
  padding: 1rem;
}

form > button {
  background-color: #4273f4;
  border: none;
  padding: 1rem;
  color: #fff;
  font-size: 16px;
  letter-spacing: 1px;
  cursor: pointer;
}

.q {
  height: 40px;
  margin: 10px 0 0 10px;
}

.option {
  padding: 0.5em 0;
}
.score {
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}
.score span {
  padding: 20px;
  background-color: orangered;
  color: white;
  border-radius: 50%;
}
</style>
<script setup lang="ts">
import { ref } from 'vue'

interface QuestionType {
  question: string
  answers: string[]
  correctAnswer: string
}

const questions = ref<QuestionType[]>([
  {
    question: 'what is 1 + 1 ',
    answers: ['2', '3', '6', '7'],
    correctAnswer: '2'
  },
  {
    question: 'what is 2 * 2 ',
    answers: ['2', '3', '4', '10'],
    correctAnswer: '4'
  },
  {
    question: 'what is 10 / 5 ',
    answers: ['2', '5', '6', '7'],
    correctAnswer: '2'
  },
  {
    question: 'what is 3 + 2',
    answers: ['5', '3', '6', '7'],
    correctAnswer: '5'
  },
  {
    question: 'what is 7 - 6  ',
    answers: ['1', '3', '6', '7'],
    correctAnswer: '1'
  }
])

const score = ref<number>(0)
const compteurQuestion = ref<number>(0)
const reponse = ref<string>('')
const selectedQuestion = ref(questions.value[0])
const montrerScore = ref<boolean>(false)
let message = ref<string>('')

const submitReponses = () => {
  if (selectedQuestion.value.correctAnswer === reponse.value) {
    score.value += 10
  }

  if (compteurQuestion.value < questions.value.length - 1) {
    compteurQuestion.value++
    selectedQuestion.value = questions.value[compteurQuestion.value]
  } else {
    montrerScore.value = true
    message.value = score.value >= 25 ? 'Felicitations 😀' : 'dommage 😞'
  }

  reponse.value = ''
}
</script>
