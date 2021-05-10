<template>
  <div> 
    <div class="answer_container">{{ answerToPass }}</div>
  </div>
</template>

<script>
export default {
  name: "Answer",
  props: {
    answerToPass: {
      type: String,
      required: true
    }
  }
}
</script>

<style lang="scss" scoped>
  .answer_container {
    position: relative;
    width: 380px;
    color: white;
    padding: 20px 40px;
    border-top: 3px solid white;
    border-bottom: 3px solid white;
    border-radius: 5px;
    margin-left: 5%;
    margin-right: 5%;
  }

  .answer_container::before {
    position: absolute;
    left: -21px;
    top: 5px;
    content: "";
    width: 44px;
    height: 44px;
    transform: rotate(45deg);
    border-bottom: 3px solid white;
    border-left: 3px solid white;
    border-radius: 5px;
  }
  .answer_container::after {
    position: absolute;
    right: -21px;
    top: 5px;
    content: "";
    width: 44px;
    height: 44px;
    transform: rotate(-135deg);
    border-bottom: 3px solid white;
    border-left: 3px solid white;
    border-radius: 5px;
  }
</style>