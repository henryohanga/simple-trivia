<template>
  <div class="trivia">
    <div v-if="loading">Loading...</div>
    <div v-if="error">{{ error }}</div>
    <h3>{{ (questions.length && questions[0].category) || "Quiz" }}</h3>
    <QuestionBox
      v-for="question in questions"
      :key="question.id"
      :question="question"
    ></QuestionBox>
  </div>
</template>

<script>
import axios from "axios";

import QuestionBox from "@/components/QuestionBox";

export default {
  components: { QuestionBox },
  data() {
    return {
      loading: false,
      error: null,
      questions: []
    };
  },

  created() {
    this.fetchQuestions();
  },
  watch: {
    //   call again the method if the route changes
    // "$route": "fetchQuestions"
  },
  methods: {
    fetchQuestions() {
      this.loading = true;
      this.error = null;
      axios
        .get(
          `https://opentdb.com/api.php?amount=20&category=${this.$route.params.id}&type=multiple`
        )
        .then(res => {
          this.loading = false;
          this.questions = res.data.results;
        })
        .catch(err => {
          this.loading = false;
          this.error = err;
        });
    }
  }
};
</script>

<style scoped></style>
