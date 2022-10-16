<template>
<div>
  <h1 v-html="this.question"></h1>
  <br>
  <p>{{this.correctAnswer}}</p>

  <label for="">true</label>
  <input type="radio" name="options" value="true">
  <label for="">false</label>
  <input type="radio" name="options"  value="false">
  <button type="button">send</button>
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
    }
  },
  computed: {
    answers() {
      let answers = JSON.parse(JSON.stringify(this.incorrectAnswer))
      answers.splice(Math.round(Math.random() * answers.length), 0, this.correctAnswer)
      return answers
    }
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
