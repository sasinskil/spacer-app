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
      <Item
        v-for="item in results"
        :item="item"
        :key="item.data[0].nasa_id"
        @click.native="handleModalOpen(item)"
      />
    </div>
    <div class="loading" v-if="step === 1 && loading">
      <div></div>
      <div></div>
      <div></div>
      <div></div>
    </div>

    <Modal v-if="modalOpen" :item="modalItem" @closeModal="modalOpen = false" />
  </div>
</template>

<script>
import axios from "axios";
import debounce from "lodash.debounce";
import Header from "@/components/Header.vue";
import SearchInput from "@/components/SearchInput.vue";
import HeroImage from "@/components/HeroImage.vue";
import Item from "@/components/Item.vue";
import Modal from "@/components/Modal.vue";

const API = "https://images-api.nasa.gov/search";

export default {
  name: "App",
  components: {
    Header,
    SearchInput,
    HeroImage,
    Item,
    Modal
  },
  data() {
    return {
      modalOpen: false,
      modalItem: null,
      loading: false,
      step: 0,
      searchValue: "",
      results: []
    };
  },
  methods: {
    handleModalOpen(item) {
      this.modalOpen = true;
      this.modalItem = item;
    },

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

.loading {
  margin-top: 7rem;
  display: inline-block;
  position: relative;
  width: 64px;
  height: 64px;
  color: #1e3d4a;

  @media screen and(min-width: 768px) {
    width: 84px;
    height: 84px;
  }
}
.loading div {
  box-sizing: border-box;
  display: block;
  position: absolute;
  width: 51px;
  height: 51px;
  margin: 6px;
  border: 6px solid #1e3d4a;
  border-radius: 50%;
  animation: loading 1.2s cubic-bezier(0.5, 0, 0.5, 1) infinite;
  border-color: #1e3d4a transparent transparent transparent;

   @media screen and(min-width: 768px) {
    width: 84px;
    height: 84px;
  }
}
.loading div:nth-child(1) {
  animation-delay: -0.45s;
}
.loading div:nth-child(2) {
  animation-delay: -0.3s;
}
.loading div:nth-child(3) {
  animation-delay: -0.15s;
}
@keyframes loading {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
