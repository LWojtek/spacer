<template>
  <div class="claim__wrapper">
    <h1 class="claim">SPACER</h1>
    <p class="subclaim">
      Begin your journey through our amazing galaxy and discover places you never even heard of.
    </p>
    <p class="subclaim">
      Type anything space-related to start.
    </p>
  </div>
</template>

<script>
export default {
  name: 'Claim',
};
</script>

<style lang="scss" scoped>
  .claim__wrapper {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
    color: #fff;
  }

  .claim {
    font-size: 50px;
    margin: 0;
    text-shadow: 0 0 5px #000;

    @media (min-width: 768px) {
      font-size: 80px;
      letter-spacing: 10px;
    }
    @media (min-width: 1024px) {
      font-size: 100px;
      letter-spacing: 10px;
    }
  }

  .subclaim {
    margin-top: 20px 0 0 0;
    font-size: 13px;
    font-weight: 400;

        @media (min-width: 768px) {
      font-size: 20px;
      letter-spacing: 1px;
          width: 550px;

    }
  }
</style>
