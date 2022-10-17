<template>
<div>

  <template v-if="this.question">

    <h1 v-html="this.question"></h1>
    <br>
    
  
    <template v-for="(answer, index) in this.answers " v-bind:key="index">
  
      <input type="radio" name="options" :value="answer" v-model="this.chosen_answer">
      <label v-html="answer"></label>
    </template>
   
    <button @click="this.submitAnswer()" type="button">send</button>
  </template>
  
</div>
</template>

<script>



export default {
  name: 'App',

  data() {
    return {
      question: undefined,
      incorrectAnswer: undefined,
      correctAnswer: undefined,
      chosen_answer : undefined,
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
      
      if (!this.chosen_answer) {
        alert("wrong")
      } else {
        if (this.chosen_answer === this.correctAnswer) {
          alert("bonne reponse")
        }
      }
      
    },
  },

  created() {
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
  
}

</script>

<style>

</style>
