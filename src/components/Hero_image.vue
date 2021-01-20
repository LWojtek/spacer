<template>
<img class="heroImage"/>
</template>

<script>

export default {
  name: 'heroImage',
};
</script>

<style lang="scss" scoped>
  .heroImage {
    position: fixed;
    top: 0;
    z-index: -1;
    width: 100%;
    height: 100vh;
    background-image: url('../assets/hero1.jpg');
    background-repeat: no-repeat;
    object-fit: cover;
    background-position: 49% 0%;

    // &::after {
    // content: "";
    // background: rgba(0,0,0,1);
    // position: absolute;
    // z-index: 1;
    // top: 0;
    // left: 0;
    // width: 100%;
    // height: 100vh;
    // }
  }
</style>
