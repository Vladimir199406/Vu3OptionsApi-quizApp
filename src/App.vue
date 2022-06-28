<template>
  <div class="ctr">
    <transition name="fade" mode="out-in">
      <questions
        v-if="questionsAnswered < questions.length"
        :questions="questions"
        :questionsAnswered="questionsAnswered"
        @question-answered="questionAnswered"
      ></questions>
      <result v-else :results="results" :totalCorrect="totalCorrect"></result>
    </transition>
    <button
      type="button"
      class="reset-btn"
      @click.prevent="reset"
      v-if="this.questionAnswered === questions.length"
    >
      Reset
    </button>
  </div>
</template>

<script>
import Questions from "./components/Questions.vue";
import Result from "./components/Result.vue";
import QuestionMixin from "./mixins/QuestionsMixin"

export default {
  name: "App",
  components: {
    Questions,
    Result,
  },
  data() {
    return {
      questionsAnswered: 0,
      totalCorrect: 0,
    };
  },
  mixins: [QuestionMixin],
  methods: {
    questionAnswered(is_correct) {
      is_correct && this.totalCorrect++;
      this.questionsAnswered++;
    },
    reset() {
      this.questionAnswered = 0;
      this.totalCorrect = 0;
    },
  },
};
</script>

<style>
</style>
