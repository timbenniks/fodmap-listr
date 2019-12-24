<template>
  <main role="main">
    <div class="text-filter">
      <input
        type="text"
        name="filter"
        placeholder="Filter foods by name"
        v-model="filter"
        v-on:focus="filterFocus"
      />
    </div>
    <ul>
      <li
        v-for="food in filteredFoods"
        :data-status="food.status"
        :data-category="food.category"
        :key="`${Math.random()}-${food.name}`"
      >
        <span class="name">{{ food.name }}</span>
        <span class="note" v-if="food.note">{{ food.note }}</span>
      </li>
    </ul>
  </main>
</template>

<script>
import foods from "../foods.json";
import Fuse from "fuse.js";

export default {
  name: "fodmap",
  data() {
    return {
      foods: foods.foods,
      categories: foods.categories,
      status: foods.status,
      filter: ""
    };
  },
  created() {
    var options = {
      shouldSort: true,
      threshold: 0.3,
      location: 0,
      distance: 50,
      maxPatternLength: 32,
      minMatchCharLength: 2,
      keys: ["name"]
    };

    this.fuse = new Fuse(this.foods, options);
  },
  computed: {
    filteredFoods() {
      if (this.filter.trim() === "") {
        return this.foods;
      } else {
        return this.fuse.search(this.filter.trim());
      }
    }
  },
  methods: {
    filterFocus() {
      window.scrollTo(0, 0);
    }
  }
};
</script>

<style scoped lang="scss">
.text-filter {
  position: sticky;
  position: -webkit-sticky;
  margin: 0;
  padding: 0;
  top: 0;
  left: 0;
  width: 100%;
  overflow: hidden;
  background: #fff;
  border-bottom: 2px solid #42b983;

  input {
    width: calc(100% - 2em);
    font-size: 15px;
    padding: 1em;
    background: #fff;
    border: none;
    border-radius: 0;
    -webkit-appearance: none;
    -moz-appearance: none;
    appearance: none;

    &:focus {
      outline: none;
      background: #f9f9f9;
    }
  }
}

li {
  padding: 0.5em;
  border-bottom: 1px solid #ddd;

  &[data-status="1"] {
    background: #fff0f0;
  }

  &[data-status="0"] {
    background: #f0fff4;
  }

  span {
    display: block;

    &.note {
      font-size: 11px;
      color: #777;
    }
  }
}
</style>
