<template>
  <div class="header-container">
    <h1 class="header">SPACER</h1>
    <p class="paragraph">
      Begin your journey through our amazing galaxy,
      and discover places you never even heard of.
    </p>
    <p class="paragraph">Type anything space-related to start.</p>
  </div>
</template>

<script>
export default {
  name: "Header"
};
</script>

<style lang="scss" scoped>

.header-container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
}

.header {
    font-size: 3rem;
    margin: 0;
}

.paragraph {
    margin-top: 1.3rem;
    font-size: 0.8rem;
}

</style>
