<template>
  <div class="search-container">
    <HeroImage />
    <Header />
    <SearchInput v-model="searchValue" @input="handleInput"/>
  </div>
</template>

<script>
import axios from "axios";
import debounce from "lodash.debounce";
import Header from "@/components/Header.vue";
import SearchInput from "@/components/SearchInput.vue";
import HeroImage from "@/components/HeroImage.vue";

const API = "https://images-api.nasa.gov/search";

export default {
  name: "App",
  components: {
    Header,
    SearchInput,
    HeroImage
  },
  data() {
    return {
      searchValue: "",
      results: []
    };
  },
  methods: {
    handleInput: debounce(function() {
      console.log(this.searchValue);
      axios
        .get(`${API}?q=${this.searchValue}&media_type=image`)
        .then(resp => (this.results = resp.data.collection.items))
        .catch(error => {
          console.log(error);
        });
    }, 500)
  }
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css?family=Montserrat:200,400,700&display=swap&subset=latin-ext");

* {
  box-sizing: border-box;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

body {
  font-family: "Montserrat", sans-serif;
  color: #fff;
  margin: 0;
  padding: 0;
}

.search-container {
  margin: 0;
  width: 100%;
  min-height: 100vh;
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

  &__input {
    text-align: center;
    padding: 0.5rem;
    border: none;
    background: none;
    border-bottom: 1px solid #fff;
  }
}
</style>
