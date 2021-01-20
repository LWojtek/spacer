<template>
        <div class="search__wrapper">
            <!-- <label for="search">Search</label> -->
            <input
            name="search"
            :class="{ dark }"
            id="search"
            :value="value"
            @input="handleChange"
          />
      </div>
</template>

<script>
export default {
  name: 'searchInput',
  props: {
    value: {
      type: String,
      required: true,
    },
    dark: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    handleChange(e) {
      this.$emit('input', e.target.value);
    },
  },
};
</script>

<style lang="scss" scoped>

.search__wrapper {
  display: flex;
  align-items: center;;
  flex-direction: column;
  width: 250px;
  margin-top: 50px;

      label {
      font-family: Arial, Helvetica, sans-serif;
      text-align: center;
    }

    input {
      height: 35px;
      border: none;
      border-bottom: 2px solid #fff;
      background-color: transparent;
      outline: none;
      color: #fff;
      font-size: 16px;
      font-weight: 300;
      text-transform: uppercase;
      text-align: center;
      transition: box-shadow .4s;
      margin: 50px 0px 80px 0;;

      @media (min-width: 1024px) {
        width: 500px;
      }

      &:focus {
        box-shadow: 0 2px 20px -5px rgba(255,255,255, 1);
      }
    }
    .dark {
      color: #1e3d4a;
      border-bottom-color: #1e3d4a;
    }
}

</style>
