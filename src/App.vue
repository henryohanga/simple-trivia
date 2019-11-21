<template>
  <div id="app">
    <TriviaNavbar
      :answered="correctlyAnswered"
      :total="totalAnswered"
    ></TriviaNavbar>
    <div class="container mt-5 pt-4">
      <router-view />
    </div>
  </div>
</template>

<script>
import TriviaNavbar from "@/components/TriviaNavbar";

export default {
  components: {
    TriviaNavbar
  },
  data() {
    return {
      correctlyAnswered: 0,
      totalAnswered: 0
    };
  },
  methods: {
    updateScore(obj) {
      this.totalAnswered++;

      if (obj.correct) {
        this.correctlyAnswered++;
      }
    }
  },

  mounted() {
    this.$root.$on("question-answered", this.updateScore);
  }
};
</script>

<style></style>
