<template>
  <div class="item-container">
    <div :style="style" class="item"></div>
  </div>
</template>

<script>
export default {
  name: "Item",
  props: {
    item: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      photo: this.item.links[0].href,
      title: this.item.data[0].title
    };
  },
  computed: {
    style() {
      return `backgroundImage: url("${this.photo}")`;
    }
  }
};
</script>

<style lang="scss" scoped>
.item {
  width: 40vw;
  height: 250px;
  background-size: cover;
  background-repeat: no-repeat;
  background-position: 50%;
  border-radius: 0.3rem;

  @media screen and(min-width: 768px) {
    width: 25vw;
  }
}
</style>
