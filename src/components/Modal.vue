<template>
  <div class="outerWrapper">
    <div class="innerWrapper">
      <div class="photo__wrapper">
        <div class="photo">
            <img :src="photo" />
        </div>
        </div>
        <div class="description">
          <h2 class="title">{{title}}</h2>
          <p class="description">
            {{ description }}
          </p>
        </div>
    </div>
    <div class="close" @click="$emit('closeModal')"/>
  </div>
</template>

<script>
export default {
  name: 'Modal',
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      photo: null,
      title: null,
      description: null,
    };
  },
  mounted() {
    this.photo = this.item.links[0].href;
    this.title = this.item.data[0].title;
    this.description = this.item.data[0].description.substring(0, 200);
  },
};
</script>

<style lang="scss" scoped>
  .outerWrapper {
    background: #f6f6f6;
    max-width: 100%;
    height: 100%;
    position: fixed;
    top: 0;
    left: 0;

    @media(min-width: 1024px) {
      max-width: 70%;
      height: 60%;
      left: 0;
      right: 0;
      bottom: 0;
      top:0%;
      margin: auto;
      box-shadow: 0 30px 30px -10px rgba(0,0,0, .3);
          }

    }

  .close {
    position: absolute;
    padding: 30px;
    width: 30px;
    height: 30px;
    right: 0px;
    top: 0px;
    cursor: pointer;

      &::before,
      &::after {
        position: absolute;
        top: 20px;
        right: 20px;
        content: '';
        width: 20px;
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

  .innerWrapper {
      display: flex;
      height: 100%;
      padding: 20px;
      justify-content: center;
      align-items: center;
      flex-direction: column;

    @media(min-width: 1024px) {
      flex-direction: row;
        }

  }

      // @media(min-width: 1024px) {
      //     .photo{
      //       flex-basis: 70%;
      //     }

      //     .description {
      //       flex-basis: 30%;
      //     }
      //     }

  .photo__wrapper {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100%;
    height: 100%;
         img {
       width: 100%;
        }
  }

  .photo {
  flex-basis: 100%;

  @media(min-width: 1024px) {
      flex-basis: 80%;
    }
  }
  .description {
    color: #333;
    padding: 20px 0;
    flex-basis: 60%;
  }

  .title{
    color: #1e3d4a;
    margin:0;
  }

</style>
