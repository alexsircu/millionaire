<template>
  <div class="button_container">
    <button class="next_turn" @click="buttonClicked">{{ buttonTextToPass }}</button>
  </div>
</template>

<script>
export default {
  name: "Button",
  props: {
    buttonTextToPass: {
      type: String,
      required: true
    }
  },
  methods: {
    buttonClicked() {
      const self = this;
      self.$emit('buttonClicked');
    }
  }
}
</script>

<style lang="scss" scoped>
  .next_turn {
    color: white;
    background: none;
    font-size: 18px;
    padding: 10px 30px;
    border: 2px solid white;
    border-radius: 5px;
    margin-top: 30px;
    margin-right: 40px;
    cursor: pointer;
  }
</style>