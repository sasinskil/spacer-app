<template>
  <div :class="[{flexStart: step === 1}, 'search-container']">
    <transition name="move">
      <span class="logo" v-if="step === 1">SPACER</span>
    </transition>
    <transition name="fade">
      <HeroImage v-if="step === 0" />
    </transition>
    <Header v-if="step === 0" />
    <SearchInput v-model="searchValue" @input="handleInput" :dark="step === 1" />
    <div class="results" v-if="results && !loading && step === 1">
      <Item v-for="item in results" :item="item" :key="item.data[0].nasa_id" />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import debounce from "lodash.debounce";
import Header from "@/components/Header.vue";
import SearchInput from "@/components/SearchInput.vue";
import HeroImage from "@/components/HeroImage.vue";
import Item from "@/components/Item.vue";

const API = "https://images-api.nasa.gov/search";

export default {
  name: "App",
  components: {
    Header,
    SearchInput,
    HeroImage,
    Item
  },
  data() {
    return {
      loading: false,
      step: 0,
      searchValue: "",
      results: []
    };
  },
  methods: {
    handleInput: debounce(function() {
      this.loading = true;
      axios
        .get(`${API}?q=${this.searchValue}&media_type=image`)
        .then(resp => {
          this.results = resp.data.collection.items;
          this.loading = false;
          this.step = 1;
        })
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

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}

.move-enter-active,
.move-leave-active {
  transition: margin-top 0.3s ease;
}
.move-enter,
.move-leave-to {
  margin-top: -2rem;
}

.search-container {
  position: relative;
  margin: 0;
  width: 100%;
  min-height: 100vh;
  padding: 2rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  &.flexStart {
    justify-content: flex-start;
  }
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

.logo {
  position: absolute;
  top: 1.5rem;
  font-weight: 700;
  color: #1e3d4a;

  @media screen and(min-width: 768px) {
    font-size: 1.2rem;
  }

  @media screen and(min-width: 1024px) {
    font-size: 1.4rem;
  }
}

.results {
  margin-top: 3rem;
  color: #1e3d4a;
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-gap: 1rem;

  @media screen and(min-width: 768px) {
    grid-gap: 1.5rem;
    grid-template-columns: 1fr 1fr 1fr;
  }
}
</style>
