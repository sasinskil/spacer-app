<template>
  <div class="searchInput-container">
    <div class="search">
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
  name: "SearchInput"
};
</script>

<style lang="scss" scoped>

.searchInput-container {
  width: 100%;
  margin: 2.5rem 0 0;
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
    border-bottom: 1px solid #fff;;
  }
}
</style>
