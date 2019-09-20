<template>
  <div class="heroImage-container"></div>
</template>

<script>
export default {
  name: "HeroImage"
};
</script>

<style lang="scss" scoped>
.heroImage-container {
  width: 100%;
  min-height: 100vh;
  position: fixed;
  z-index: -1;
  background-image: url("../assets/heroimage.jpg");
  background-repeat: no-repeat;
  background-size: cover;
  background-position: 80% 0%;

  &::after {
      position: absolute;
      content: "";
      top: 0;
      left: 0;
      display: block;
      z-index: 1;
      width: 100%;
      height: 100vh;
      background-color: black;
      opacity: 0.2;
  }
}
</style>
