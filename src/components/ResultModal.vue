<template>
     <div  class="fixed pin flex justify-center items-center z-10">
      <div class="absolute pin bg-green opacity-50"> </div>
      <div class=" relative bg-white rounded p-10 border shadow-lg w-3/4 px-10 py-20 flex flex-col justify-center"> 
         <h3 class="mb-4 text-5-xl" v-if="isCorrect">I KNEW YOU WERE BRIGHT 🎉🎉</h3>
         <h3 class="mb-4 text-5-xl" v-if="!isCorrect"> wrong answer 😥😢<p class="text-lg pt-3"> The Correct answer should be : <strong> {{ question.correct_answer }} </strong> </p> </h3>
         <button @click="handleNextButton" class="text-base" :class="[isCorrect ? 'bg-green-lighter p-5 border border-green rounded hover:bg-green-lightest' : 'bg-red-lighter p-5 border border-red rounded hover:bg-red-lightest']"> Next Question 👉🏽 </button>

      </div>
      </div>
  
</template>

<script>
export default {
  props: ['isCorrect', 'question'],
  methods:{
    handleNextButton(){
      this.$emit('goNext')
    },
    

  }

}
</script>

<style>

</style>
