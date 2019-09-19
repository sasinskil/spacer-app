<template>
  <div class="container">
    <div class="search">
      <label class="search__label" for="search">Search</label>
      <input
        class="search__input"
        type="text"
        id="search"
        name="search"
        v-model="searchValue"
        @input="handleInput"
      />
      <ul>
        <li v-for="item in results" :key="item.data[0].nasa_id">
          <p>{{item.data[0].title}}</p>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import debounce from "lodash.debounce";

const API = "https://images-api.nasa.gov/search";

export default {
  name: "Search",
  data() {
    return {
      searchValue: "",
      results: []
    };
  },
  methods: {
    handleInput: debounce(function() {
      axios
        .get(`${API}?q=${this.searchValue}&media_type=image`)
        .then((resp) => (this.results = resp.data.collection.items))
        .catch((error) => {
          console.log(error);
        });
    }, 500),
  },
};
</script>

<style lang="scss" scoped>
.container {
  width: 100%;
  margin: 0;
  padding: 2rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.search {
  display: flex;
  flex-direction: column;
  width: 250px;

  &__label {
    text-align: left;
  }

  &__input {
    text-align: center;
    padding: 0.5rem;
    border: none;
    border-bottom: 1px solid black;
  }
}
</style>
