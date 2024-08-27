<template>
  <div>
    <div class="wrapper">
      <div v-if="!debutQuiz" class="starter">
        <h2>QUIZ IVOIRE</h2>
        <button @click="commercerQuiz">Commencer</button>
      </div>
      <transition v-if="debutQuiz && !montrerScore" name="fade">
        <form @submit.prevent="submitReponses" v-if="selectedQuestion" :key="compteurQuestion">
          <div class="timer">
            <span>{{ tempsRestant }}s</span>
          </div>
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
          <button type="submit">repondre</button>
        </form>
      </transition>
      <div v-else class="score">
        <div class="confetti">
          <div class="confetti-piece"></div>
          <div class="confetti-piece"></div>
          <div class="confetti-piece"></div>
          <div class="confetti-piece"></div>
          <div class="confetti-piece"></div>
          <div class="confetti-piece"></div>
          <div class="confetti-piece"></div>
          <div class="confetti-piece"></div>
          <div class="confetti-piece"></div>
          <div class="confetti-piece"></div>
          <div class="confetti-piece"></div>
          <div class="confetti-piece"></div>
          <div class="confetti-piece"></div>
          <div class="confetti-piece"></div>
          <div class="confetti-piece"></div>
          <div class="confetti-piece"></div>
          <div class="confetti-piece"></div>
          <div class="confetti-piece"></div>
          <div class="confetti-piece"></div>
        </div>
        <div v-if="debutQuiz" class="starter">
          <button @click="commercerQuiz">Recommencer</button>
          <h3>
            {{ message }} votre score est de <span>{{ score }}/{{ questions.length * 10 }}</span>
          </h3>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.wrapper {
  height: 360px;
  width: 400px;
  background-color: #fff;
  border-radius: 10px;
  overflow: hidden;
  padding: 0;
}
.timer {
  display: flex;
  justify-content: flex-end;
  align-items: center;
}
.timer span {
  padding: 10px;
  color: #fff;
  background-color: #24fa36;
  margin: 10px 10px 0 0;
  border-radius: 50%;
}

.starter {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100%;
}
.starter button {
  padding: 10px;
  background-color: #f78000;
  color: #fff;
  box-shadow: 2px 0px 0px 2px rgba(0, 0, 0, 0.471);
  border: 0;
  border-radius: 5px;
  cursor: pointer;
  z-index: 2;
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
  background-color: #51db5c;
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
  padding: 5px;
  background-color: #f78000;
  color: white;
  border-radius: 50%;
}

.confetti {
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  width: 240px;
  height: 100%;
  overflow: hidden;
  z-index: 1;
}
.confetti-piece {
  position: absolute;
  width: 10px;
  height: 20px;
  background-color: #f78000;
  top: 0;
  opacity: 0;
  animation: makeItRain 3000ms infinite linear;
}

.confetti-piece:nth-child(1) {
  left: 7%;
  transform: rotate(-10deg);
  animation-delay: 182ms;
  animation-duration: 2000ms;
}

.confetti-piece:nth-child(2) {
  left: 14%;
  transform: rotate(20deg);
  animation-delay: 161ms;
  animation-duration: 2076ms;
}

.confetti-piece:nth-child(3) {
  left: 21%;
  transform: rotate(-51deg);
  animation-delay: 481ms;
  animation-duration: 2103ms;
}

.confetti-piece:nth-child(4) {
  left: 28%;
  transform: rotate(61deg);
  animation-delay: 334ms;
  animation-duration: 1008ms;
}

.confetti-piece:nth-child(5) {
  left: 35%;
  transform: rotate(-52deg);
  animation-delay: 302ms;
  animation-duration: 1776ms;
}

.confetti-piece:nth-child(6) {
  left: 42%;
  transform: rotate(38deg);
  animation-delay: 180ms;
  animation-duration: 1168ms;
}

.confetti-piece:nth-child(7) {
  left: 49%;
  transform: rotate(11deg);
  animation-delay: 395ms;
  animation-duration: 1200ms;
}

.confetti-piece:nth-child(8) {
  left: 56%;
  transform: rotate(49deg);
  animation-delay: 14ms;
  animation-duration: 1887ms;
}

.confetti-piece:nth-child(9) {
  left: 63%;
  transform: rotate(-72deg);
  animation-delay: 149ms;
  animation-duration: 1805ms;
}

.confetti-piece:nth-child(10) {
  left: 70%;
  transform: rotate(10deg);
  animation-delay: 351ms;
  animation-duration: 2059ms;
}

.confetti-piece:nth-child(11) {
  left: 77%;
  transform: rotate(4deg);
  animation-delay: 307ms;
  animation-duration: 1132ms;
}

.confetti-piece:nth-child(12) {
  left: 84%;
  transform: rotate(42deg);
  animation-delay: 464ms;
  animation-duration: 1776ms;
}

.confetti-piece:nth-child(13) {
  left: 91%;
  transform: rotate(-72deg);
  animation-delay: 429ms;
  animation-duration: 1818ms;
}

.confetti-piece:nth-child(14) {
  left: 94%;
  transform: rotate(-72deg);
  animation-delay: 429ms;
  animation-duration: 818ms;
}

.confetti-piece:nth-child(15) {
  left: 96%;
  transform: rotate(-72deg);
  animation-delay: 429ms;
  animation-duration: 2818ms;
}

.confetti-piece:nth-child(16) {
  left: 98%;
  transform: rotate(-72deg);
  animation-delay: 429ms;
  animation-duration: 2818ms;
}

.confetti-piece:nth-child(17) {
  left: 50%;
  transform: rotate(-72deg);
  animation-delay: 429ms;
  animation-duration: 2818ms;
}

.confetti-piece:nth-child(18) {
  left: 60%;
  transform: rotate(-72deg);
  animation-delay: 429ms;
  animation-duration: 1818ms;
}

.confetti-piece:nth-child(odd) {
  background-color: #f78000;
}

.confetti-piece:nth-child(even) {
  z-index: 1;
}

.confetti-piece:nth-child(4n) {
  width: 6px;
  height: 14px;
  animation-duration: 4000ms;
  background-color: #24fa36;
}

.confetti-piece:nth-child(5n) {
  width: 3px;
  height: 10px;
  animation-duration: 4000ms;
  background-color: #ffffff;
}

.confetti-piece:nth-child(3n) {
  width: 4px;
  height: 12px;
  animation-duration: 2500ms;
  animation-delay: 3000ms;
  background-color: #51db5c;
}

.confetti-piece:nth-child(3n-7) {
  background-color: hsl(0, 0%, 100%);
}

@keyframes makeItRain {
  from {
    opacity: 0;
  }

  50% {
    opacity: 1;
  }

  to {
    transform: translateY(350px);
  }
}

/* Transition fade */
/* Transition fade */
.fade-enter-active,
.fade-leave-active {
  transition:
    transform 0.6s ease,
    background-color 0.6s ease;
  transform-style: preserve-3d;
}

.fade-enter, .fade-leave-to /* .fade-leave-active in <2.1.8 */ {
  transform: rotateY(-90deg);
  background-color: #f78000;
}
</style>

<script setup lang="ts">
import { onBeforeUnmount, onMounted, ref, watch } from 'vue'

interface QuestionType {
  question: string
  answers: string[]
  correctAnswer: string
  tempsReponse: number
}
// mettre en cache la traduction
const questionsCache: Record<string, string> = {}
const questions = ref<QuestionType[]>([])

// Traduire les données en français
const cacheExpiration: Record<string, number> = {}
const CACHE_DURATION = 60 * 60 * 1000 // 1 heure en millisecondes

const translateText = async (
  text: string,
  sourceLang = 'en',
  targetLang = 'fr'
): Promise<string> => {
  const cacheKey = `${text}_${sourceLang}_${targetLang}`
  const now = Date.now()

  // Vérifier si la traduction est dans le cache et n'est pas expirée
  if (questionsCache[cacheKey] && now - cacheExpiration[cacheKey] < CACHE_DURATION) {
    return questionsCache[cacheKey]
  }

  try {
    const response = await fetch(
      `https://api.mymemory.translated.net/get?q=${encodeURIComponent(text)}&langpair=${sourceLang}|${targetLang}`
    )
    const data = await response.json()
    const translatedText = data.responseData.translatedText

    // Stocker la traduction dans le cache avec une expiration
    questionsCache[cacheKey] = translatedText
    cacheExpiration[cacheKey] = now

    return translatedText
  } catch (error) {
    console.error('Erreur lors de la traduction:', error)
    return text
  }
}

const fetchAndTranslateQuestions = async (): Promise<QuestionType[]> => {
  try {
    const response = await fetch('https://opentdb.com/api.php?amount=2&category=18&type=multiple')
    const data = await response.json()

    const translatedQuestions = await Promise.all(
      data.results.map(async (q) => {
        const question = await translateText(q.question)
        const correctAnswer = await translateText(q.correct_answer)
        const incorrectAnswers = await Promise.all(
          q.incorrect_answers.map((answer) => translateText(answer))
        )

        return {
          question, // Question traduite
          answers: [...incorrectAnswers, correctAnswer].sort(() => Math.random() - 0.5), // Réponses traduites mélangées
          correctAnswer, // Réponse correcte traduite
          tempsReponse: 20 // Temps de réponse en secondes
        }
      })
    )

    questions.value = translatedQuestions
    return translatedQuestions
  } catch (error) {
    console.error('Erreur lors de la récupération ou de la traduction des questions :', error)
    return []
  }
}

fetchAndTranslateQuestions().then((translatedQuestions) => {
  selectedQuestion.value = translatedQuestions[0]
})

// Commencer le quiz
const debutQuiz = ref<boolean>(false)
const commercerQuiz = () => {
  debutQuiz.value = true
  selectedQuestion.value = questions.value[0]
  compteurQuestion.value = 0
  montrerScore.value = false
  resetTimer()
}

const score = ref<number>(0)
const compteurQuestion = ref<number>(0)
const reponse = ref<string>('')
const selectedQuestion = ref<QuestionType | null>(null)
const montrerScore = ref<boolean>(false)
let message = ref<string>('')

// Changer de question
const passerQuestionSuivante = () => {
  if (compteurQuestion.value < questions.value.length - 1) {
    compteurQuestion.value++
    selectedQuestion.value = questions.value[compteurQuestion.value]
  } else {
    montrerScore.value = true
    message.value =
      score.value >= (questions.value.length * 10) / 2 ? 'Félicitations 😀' : 'Dommage 😞'
    resetTimer()
  }
}

// Minuteur
const tempsRestant = ref<number>(20)
let intervalle: number | null = null

const startTimer = () => {
  tempsRestant.value = selectedQuestion.value?.tempsReponse || 20
  intervalle = window.setInterval(() => {
    if (tempsRestant.value > 0) {
      tempsRestant.value--
    } else {
      clearInterval(intervalle!)
      submitReponses()
    }
  }, 1000)
}

const resetTimer = () => {
  clearInterval(intervalle as number)
  intervalle = null
  startTimer()
}

const submitReponses = () => {
  if (selectedQuestion.value?.correctAnswer === reponse.value) {
    score.value += 10
  }
  passerQuestionSuivante()
  reponse.value = ''
}

onMounted(() => {
  startTimer()
})

onBeforeUnmount(() => {
  clearInterval(intervalle as number)
})

// Mettre à jour le timer au changement de question
watch(compteurQuestion, () => {
  resetTimer()
})
</script>
