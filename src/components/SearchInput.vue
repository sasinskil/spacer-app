<template>
  <div class="search">
    <input
      class="search__input"
      type="text"
      id="search"
      name="search"
      :class="{ dark }"
      :value="value"
      @input="handleChange"
    />
  </div>
</template>

<script>
export default {
  name: "SearchInput",
  props: {
    value: {
      type: String,
      required: true
    },
    dark: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    handleChange(e) {
      this.$emit("input", e.target.value);
    }
  }
};
</script>

<style lang="scss" scoped>
.search {
  margin-top: 3rem;
  width: 250px;

  @media screen and(max-width: 640px) {
    width: 200px;
  }

  @media screen and(min-width: 1024px) {
    margin-top: 5rem;
  }

  &__input {
    text-align: center;
    color: #fff;
    padding: 0.5rem;
    border: none;
    background: none;
    border-bottom: 1px solid #fff;
    transition: box-shadow 0.3s ease-in-out;

    @media screen and(min-width: 768px) {
      font-size: 1.2rem;
    }

    @media screen and(min-width: 1024px) {
      font-size: 1.4rem;
    }

    &:focus {
      outline: none;
      box-shadow: 0 10px 10px -9px rgba(255, 255, 255, 0.5);
    }
  }
}

.dark {
  color: #1e3d4a;
  border-bottom-color: #1e3d4a;

  &:focus {
    outline: none;
    box-shadow: 0 10px 10px -9px rgba(#1e3d4a, 0.5);
  }
}
</style>
