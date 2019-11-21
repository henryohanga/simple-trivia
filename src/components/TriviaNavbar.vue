<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="info" fixed="top">
      <div class="container">
        <b-navbar-brand href="/">Simple Trivia</b-navbar-brand>

        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

        <b-collapse id="nav-collapse" is-nav>
          <b-navbar-nav class="">
            <b-nav-item href="/">Home</b-nav-item>
            <b-nav-item :to="{ name: 'about' }">About</b-nav-item>
            <b-nav-item href="#" disabled>Score</b-nav-item>
          </b-navbar-nav>

          <b-navbar-nav>
            <b-nav-text>{{ answered }} / {{ total }}</b-nav-text>
          </b-navbar-nav>
        </b-collapse>
      </div>
    </b-navbar>
  </div>
</template>

<script>
import Vue from "vue";

import { NavbarPlugin } from "bootstrap-vue";

Vue.use(NavbarPlugin);

export default {
  name: "TriviaNavbar",
  props: ["answered", "total"]
};
</script>
