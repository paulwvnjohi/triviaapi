<template>
  <div id="app" class="container mx-auto">


    <!-- show the result modal -->
    <ResultModal :isCorrect="isCorrect" :question="question" v-if="isCorrect !== null" @goNext="getOneQuestion" />

    <div class="mx-width-sm mx-auto">
     <div class="text-4xl flex justify-end mb-8" >
      <div class="px-4 text-right text-red-light"> {{ countOfWrongAnswers }} <div class=" text-red-light text-sm"> Wrong</div> </div> 
      <div class="px-4 text-right text-green-light">  {{ countOfCorrectAnswers }} <div class=" text-green-light text-sm"> Correct </div> </div> 
    </div>
      <QuestionItem :question="question"  @questionAnswered="handleQuestionAnswered"/>
    </div>
    <div class="mt-5 text-right"> 
    <button @click="getOneQuestion" class="text-xs text-green-darker bg-green-lighter p-5 border border-green rounded hover:bg-green-lightest "> Next Question 👉🏽 </button>
   
    </div>
  
  </div> 
</template>

<script>

import QuestionItem from './components/QuestionItem'
import ResultModal from './components/ResultModal'
export default {
  name: "App",
  components: {
    QuestionItem,
    ResultModal

  },
  data() {
    return {
      question: null,
      isCorrect: null,
      countOfWrongAnswers: 0,
      countOfCorrectAnswers: 0
    };
  },
  methods: {
    getOneQuestion() {
      this.isCorrect =null,
      fetch("https://opentdb.com/api.php?amount=1&category=12")
        .then(resp => resp.json())
        .then(data => (this.question = data.results[0]));
    },
    handleQuestionAnswered(e){
       const answer = e.answer;
      //determine is answer is correct or wrong
      const isCorrect = !this.question.incorrect_answers.includes(answer)

      this.isCorrect = isCorrect;

      if (isCorrect){
        this.countOfCorrectAnswers ++
      }else{
        this.countOfWrongAnswers++
      }

    }
 
  },
 
  mounted() {
    this.getOneQuestion();
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
