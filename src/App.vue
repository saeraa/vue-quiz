<template>
  <div class="ctr">
    <transition name="fade" mode="out-in">
      <Questions v-if="questionsAnswered < questions.length" :questions="questions"
        :questionsAnswered="questionsAnswered" @question-answered="questionAnswered"></Questions>
      <Result v-else :results="results" :totalCorrect="totalCorrect"></Result>
    </transition>

    <button type="button" class="reset-btn" @click.prevent="reset"
      v-if="questionsAnswered === questions.length">Reset</button>
  </div>
</template>

<script>
import Questions from "./components/Questions.vue"
import Result from "./components/Result.vue"
export default {
  name: "App",
  components: {
    Questions, Result
  },
  methods: {
    reset() {
      this.questionsAnswered = 0
      this.totalCorrect = 0
    },
    questionAnswered(is_correct) {
      is_correct ? this.totalCorrect++ : null
      this.questionsAnswered++
    }
  },
  data() {
    return {
      questionsAnswered: 0,
      totalCorrect: 0,
      questions: [
        {
          q: 'What country has a unicorn as part of its national emblem?',
          answers: [
            {
              text: 'Scotland',
              is_correct: true
            },
            {
              text: 'Greece',
              is_correct: false
            },
            {
              text: 'America',
              is_correct: false
            },
            {
              text: 'Wakanda',
              is_correct: false
            }
          ]
        },
        {
          q: 'Where were fortune cookies invented?',
          answers: [
            {
              text: 'Beijing',
              is_correct: false
            },
            {
              text: 'Greece',
              is_correct: false
            },
            {
              text: 'San Francisco',
              is_correct: true
            },
            {
              text: 'Wakanda',
              is_correct: false
            }
          ]
        },

        {
          q: 'On average, how many seeds are located on the outside of a strawberry?',
          answers: [
            {
              text: '100',
              is_correct: false
            },
            {
              text: '200',
              is_correct: true
            },
            {
              text: '400',
              is_correct: false
            },
            {
              text: '500',
              is_correct: false
            }
          ]
        },
        {
          q: 'What is the only food that cannot go bad?',
          answers: [
            {
              text: 'Canned tuna',
              is_correct: false
            },
            {
              text: 'Dark chocolate',
              is_correct: false
            },
            {
              text: 'Honey',
              is_correct: true
            },
            {
              text: 'Peanut butter',
              is_correct: false
            }
          ]
        },
        {
          q: 'What’s the heaviest organ in the human body?',
          answers: [
            {
              text: 'Brain',
              is_correct: false
            },
            {
              text: 'Liver',
              is_correct: true
            },
            {
              text: 'Skin',
              is_correct: false
            }
          ]
        },
      ],
      results: [
        {
          min: 0,
          max: 4,
          title: "Try again!",
          desc: "Do a little more studying and you may succeed!"
        },
        {
          min: 5,
          max: 5,
          title: "Wow, you're a genius!",
          desc: "Studying has definitely paid off for you!"
        }
      ]
    }
  }
}

</script>


<style>
</style>


<!-- 
Loop through all questions and render them
Keep track of current active question and only display that question
Listen for click events on answer
Check if answer is correct
If answer is correct, keep track of how many answers are correct
Update number of questions answered
Update current active question to the next question
 -->