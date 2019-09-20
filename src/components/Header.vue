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
    font-size: 3.2rem;
    margin: 0;

    @media screen and(min-width: 768px) {
        margin-bottom: 2.5rem;
        font-size: 4rem;
    }

    @media screen and(min-width: 1024px) {
        font-size: 5rem;
    }
}

.paragraph {
    margin-top: 1.1rem;
    font-size: 0.8rem;
    max-width: 500px;
    font-weight: 200;

    @media screen and(min-width: 768px) {
        font-size: 1.1rem;
        letter-spacing: 1px;
        line-height: 1;
    }
}

</style>
