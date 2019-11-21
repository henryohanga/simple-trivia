<template>
  <b-card
    bg-variant="light"
    text-variant="dark"
    v-bind:title="question.id"
    class="mb-5 rounded-0"
  >
    <b-card-text v-html="question.question"> </b-card-text>
    <p>
      <span class="badge badge-dark rounded-0 mr-2">{{
        question.category
      }}</span>
      <span class="badge badge-secondary rounded-0 mr-2">{{
        question.difficulty
      }}</span>
    </p>

    <b-button
      block
      v-for="(answer, index) in answers"
      :variant="getVariant(index)"
      :key="answer"
      @click="setSelectedIndex(index)"
      :disabled="submitDisabled"
      class="rounded-0"
      ><span v-html="answer"></span
    ></b-button>

    <p class="text-center mt-3">
      <b-button
        variant="secondary"
        @click="validateAnswer"
        :disabled="selectedIndex === null || submitDisabled"
        class="rounded-0"
        >Submit</b-button
      >
    </p>
  </b-card>
</template>

<script>
import Vue from "vue";

import { CardPlugin } from "bootstrap-vue";
import * as _ from "lodash";

Vue.use(CardPlugin);

export default {
  name: "QuestionBox",
  props: ["question"],
  data() {
    return {
      selectedIndex: null,
      submitDisabled: false
    };
  },
  methods: {
    setSelectedIndex(index) {
      this.selectedIndex = index;
    },
    getVariant(index) {
      if (this.submitDisabled) {
        if (
          this.selectedIndex === this.correctAnsweIndex &&
          index === this.selectedIndex
        ) {
          return "success";
        } else if (this.selectedIndex === index) {
          return "danger";
        } else if (this.correctAnsweIndex === index) {
          return "outline-success";
        }
      }

      if (this.selectedIndex === index) {
        return "info";
      }

      return "outline-secondary";
    },
    validateAnswer() {
      this.submitDisabled = true;

      this.$root.$emit("question-answered", {
        correct: this.selectedIndex === this.correctAnsweIndex
      });
    }
  },
  computed: {
    answers() {
      const allAnswers = _.shuffle([
        ...this.question.incorrect_answers,
        this.question.correct_answer
      ]);

      return allAnswers;
    },
    correctAnsweIndex() {
      return this.answers.indexOf(this.question.correct_answer);
    }
  }
};
</script>

<style scoped></style>
