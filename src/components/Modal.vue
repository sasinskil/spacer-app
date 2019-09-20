<template>
  <div class="modal-container">
    <div class="main-container">
      <div class="photo">
        <img :src="photo" alt="Moon" />
      </div>
      <div class="description">
        <h2 class="description__title">{{title}}</h2>
        <p class="description__about">{{description}}</p>
      </div>
    </div>
    <div class="close" @click="$emit('closeModal')"></div>
  </div>
</template>

<script>
export default {
  name: "Modal",
  props: {
    item: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      photo: null,
      title: null,
      description: null
    };
  },
  mounted() {
    (this.photo = this.item.links[0].href),
      (this.title = this.item.data[0].title),
      (this.description = this.item.data[0].description);
  }
};
</script>

<style lang="scss" scoped>
.modal-container {
  background-color: #f6f6f6;
  color: #1e3d4a;
  border-radius: 0.3rem;
  width: 100%;
  height: 100%;
  position: fixed;
  top: 0;
  left: 0;

  @media screen and (min-width: 1024px) {
    max-width: 70%;
    height: 60%;
    left: 0;
    top: 0;
    bottom: 0;
    right: 0;
    margin: auto;
    box-shadow: 0 30px 30px -10px rgba(0, 0, 0, 0.4);
  }
}

.close {
  position: absolute;
  width: 20px;
  height: 20px;
  top: 20px;
  right: 20px;
  cursor: pointer;

  &::before,
  &::after {
    position: absolute;
    content: "";
    top: 10px;
    width: 100%;
    height: 2px;
    background: black;
    display: block;
  }

  &::before {
    transform: rotate(45deg);
  }

  &::after {
    transform: rotate(-45deg);
  }
}

.main-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 2rem;
  height: 100%;

  @media screen and (min-width: 1024px) {
    flex-direction: row;

    .photo {
      width: 50%;
      margin-right: 1.4rem;
    }
  }
}

.photo {
  width: 80%;

  @media screen and(max-width: 768px) {
    margin: 5rem 0 2rem;
  }

  img {
    width: 100%;
  }
}

.description {
  height: 100%;
  padding: 0.5rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-start;

  &__title {
    margin: 0;
  }
  &__about {
    max-height: 400px;
    overflow: auto;

    @media screen and(max-width: 454px) {
      max-width: 350px;
      max-height: 200px;
      overflow: auto;
    }

    @media screen and(min-width: 455px) and (max-width: 1023px) {
      max-width: 100%;
      max-height: 200px;
      overflow: auto;
    }

    @media screen and (min-width: 1024px) {
      max-width: 450px;
      max-height: 300px;
      overflow: auto;
    }
  }
}
</style>
