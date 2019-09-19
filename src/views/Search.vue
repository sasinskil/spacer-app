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
    </div>
  </div>
</template>

<script>

export default {
  name: "Search",
  data() {
    return {
      searchValue: ""
    };
  },
  methods: {
    handleInput() {
      console.log(this.searchValue);
    }
  }
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
    padding: 0.5rem;
    border: none;
    border-bottom: 1px solid black;
  }
}
</style>
