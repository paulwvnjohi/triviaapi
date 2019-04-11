<template>
  <div class="shadow border p-10 rounded" v-if="question">
    <h2 class="mb-5 leading-tight">{{ question.question }}</h2>
    <br>
    <ul class="list-reset">
      <li class="p-2 relative" v-for="(answer, index) in answers" :key="index">
  
        <button
          class="p-3 bg-green hover:bg-green-lighter w-full h-full rounded shadow border border-green-dark"
          v-html="answer"
          @click="questionAnswered(answer)"
        ></button>
      </li>
    </ul>
  </div>
</template>

<script>
import shuffle from "lodash.shuffle";
export default {
  props: ["question"],
  computed: {
    answers() {
      return shuffle([
        ...this.question.incorrect_answers,
        this.question.correct_answer
      ]);
    }
  },
  methods: {
    questionAnswered(answer) {
      this.$emit("questionAnswered", { question: this.question, answer });
    }
  }
};
</script>