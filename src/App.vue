<template>
    <div :class="[{ flexStart: step === 1 }, 'wrapper']">
      <transition name="slide">
        <img src="./assets/logo.png" class="logo" v-if="step === 1">
      </transition>
      <transition name="fade">
        <heroImage v-if="step === 0" />
      </transition>
      <Claim v-if="step === 0"/>
      <searchInput v-model="searchValue" @input="handleInput" :dark="step === 1"/>
      <div class="results" v-if="results && !loading && step === 1">
        <!-- eslint-disable-next-line -->
      <Item v-for="item in results" :item="item" :key="item.data[0].nasa_id" @click.native="handleModalOpen(item)"/>
      </div>
      <div class="loader" v-if="step === 1 && loading"/>
      <Modal v-if="modalOpen" :item="modalItem" @closeModal="modalOpen = false"/>
    </div>
</template>

<script>

import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue';
import searchInput from '@/components/Search_input.vue';
import heroImage from '@/components/Hero_image.vue';
import Item from '@/components/Item.vue';
import Modal from '@/components/Modal.vue';

const API = 'https://images-api.nasa.gov/search';

export default {
  name: 'Search',
  data() {
    return {
      modalOpen: false,
      modalItem: null,
      loading: false,
      step: 0,
      searchValue: '',
      results: '',
    };
  },
  components: {
    Claim,
    searchInput,
    heroImage,
    Item,
    Modal,
  },
  methods: {
    // eslint-disable-next-line
    handleModalOpen(item) {
      this.modalOpen = true;
      this.modalItem = item;
    },
    handleInput: debounce(function () {
      this.loading = true;
      console.log(this.searchValue);
      axios.get(`${API}?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.results = response.data.collection.items;
          this.loading = false;
          this.step = 1;
        })
        .catch((error) => {
          console.log(error);
        });
    }, 500),
  },
};
</script>

<style lang="scss">

@import url('https://fonts.googleapis.com/css?family=Poppins:300,400,600,800');

* {
    box-sizing: border-box;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;

  body {
    font-family: 'Poppins', Helvetica, sans-serif;
     margin: 0;
    padding: 0;
  }

  .fade-enter-active, .fade-leave-active {
    transition: opacity .5s ease;
  }

  .fade-enter, .fade-leave-to {
    opacity: 0;
  }

  .slide-enter-active, .slide-leave-active {
    transition: margin-top .5s ease;
  }

  .slide-enter, .slide-leave-to {
    margin-bottom: -110px;
  }

    .wrapper {
    display: flex;
    position: relative;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: 100%;
    min-height: 100vh;
    margin: 0;
    padding: 30px;

    &.flexStart {
      justify-content: flex-start;
    }
  }

  .loader {
  margin-top: 100px;
  display: inline-block;
  position: relative;
  width: 80px;
  height: 80px;
}
.loader:after {
  content: " ";
  display: block;
  border-radius: 50%;
  width: 0;
  height: 0;
  margin: 8px;
  box-sizing: border-box;
  border: 32px solid #1e3d4a;
  border-color: #1e3d4a transparent #1e3d4a transparent;
  animation: loading 1.2s infinite;
}
@keyframes loading {
  0% {
    transform: rotate(0);
    animation-timing-function: cubic-bezier(0.55, 0.055, 0.675, 0.19);
  }
  50% {
    transform: rotate(900deg);
    animation-timing-function: cubic-bezier(0.215, 0.61, 0.355, 1);
  }
  100% {
    transform: rotate(1800deg);
  }
}

  .logo {
    position: absolute;
    top: 30px;
    margin-bottom: 20px;

  }

  .results {
    display: grid;
    grid-template-columns: 1fr;
    grid-gap: 20px;

    @media (min-width: 468px) {
    grid-template-columns:  1fr 1fr;
    };

    @media (min-width: 768px) {
    grid-template-columns: 1fr 1fr 1fr;
    };
  }

}
</style>
