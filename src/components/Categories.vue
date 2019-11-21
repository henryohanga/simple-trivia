<template>
  <div class="categories">
    <h3>Quiz Categories</h3>
    <b-table striped bordered hover :items="categories" :fields="fields">
      <template v-slot:cell(#)="row">
        <div class="text-right">
          <b-link
            :to="`/trivia/${row.item.id}`"
            type="button"
            class="btn btn-sm btn-default"
            >Take Quiz</b-link
          >
        </div>
      </template>
    </b-table>
  </div>
</template>

<script>
import Vue from "vue";
import { TablePlugin } from "bootstrap-vue";
import { LinkPlugin } from "bootstrap-vue";

Vue.use(TablePlugin, LinkPlugin);

export default {
  props: ["categories"],

  data() {
    return {};
  },

  computed: {
    fields() {
      let categoryFields =
        (this.categories.length && Object.keys(this.categories[0])) || [];

      if (categoryFields.length) {
        categoryFields = [...categoryFields, "#"];
      }

      return categoryFields;
    }
  }
};
</script>
