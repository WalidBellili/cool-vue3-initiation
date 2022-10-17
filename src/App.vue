<template>
<div>

  <template v-if="this.question">
    <ScoreBoard />

    <h1 v-html="this.question"></h1>
    <br>
    
  
    <template v-for="(answer, index) in this.answers " v-bind:key="index">
  
      <input type="radio" :disabled="this.answer_submitted" name="options" :value="answer" v-model="this.chosenAnswer">
      <label v-html="answer"></label>
    </template>
   
    <button @click="this.submitAnswer()" v-if="!this.answer_submitted" type="button">send</button>
  </template>

  <section v-if="this.answer_submitted" class="result">
    <h4 v-if="this.chosenAnswer == this.correctAnswer" 
    v-html="'Vous avez choisi la bonne réponse était' + this.correctAnswer"></h4>
    <h4 v-else>Vous avez choisi la mauvaise réponse</h4>
    <button @click="this.getNewQuestion()">Next</button>
  </section>
  
  <HelloWorld message="efegegergz"/>
</div>

</template>

<script>


import HelloWorld from "./components/HelloWorld.vue"
import ScoreBoard from "./components/ScoreBoard.vue"


export default {
  name: 'App',
  components: {
  
    HelloWorld,
    ScoreBoard,
},

  data() {
    return {
      question: undefined,
      incorrectAnswer: undefined,
      correctAnswer: undefined,
      chosenAnswer : undefined,
      answer_submitted : false,
      winCount: 0,
      looseCount: 0,
    }
  },
  computed: {
    answers() {
      let answers = JSON.parse(JSON.stringify(this.incorrectAnswer))
      answers.splice(Math.round(Math.random() * answers.length), 0, this.correctAnswer)
      return answers
    },
  },
  methods: {
    submitAnswer() {
      this.answer_submitted = true
      if (!this.chosenAnswer) {
        alert("wrong")
      } else {
        if (this.chosenAnswer === this.correctAnswer) {
          this.winCount++
        } else {
          this.looseCount++
        }
      }
      
    },

    getNewQuestion() {
      this.answer_submitted = false,
      this.chosenAnswer = undefined,
      this.question = undefined,

      this.axios
    .get("https://opentdb.com/api.php?amount=1&category=12&difficulty=easy&type=boolean")
    .then((response) => {
      this.question = response.data.results[0].question,
      this.incorrectAnswer = response.data.results[0].incorrect_answers,
      this.correctAnswer = response.data.results[0].correct_answer
,

  console.log(response.data.results[0])

})

    }
  },

  created() {
    this.getNewQuestion()
  }
  
}

</script>

<style>

</style>
