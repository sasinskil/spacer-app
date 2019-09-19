<template>
  <div class="search-container">
    <Header />
    <SearchInput />
  </div>
</template>

<script>
import axios from "axios";
import debounce from "lodash.debounce";
import Header from '@/components/Header.vue';
import SearchInput from '@/components/SearchInput.vue';

const API = "https://images-api.nasa.gov/search";

export default {
  name: "Search",
  components: {
    Header,
    SearchInput,
  },
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

.search-container {
  margin: 0;
  width: 100%;
  min-height: 100vh;
  padding: 2rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-image: url('../assets/heroimage.jpg');
  background-repeat: no-repeat;
  background-size: cover;
  background-position: 80% 0%;
}

</style>
