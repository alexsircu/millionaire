<template>
  <div>
    <div id="section_top"> 
      <img src="../assets/millionaire.png" alt="Millionaire logo">
    </div>

    <div id="section_bottom">
      <Question />
      <Answer />
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Question from "./Question.vue";
import Answer from "./Answer.vue";

export default {
  name: "Container",
  components: {
    Question,
    Answer
  }
}
</script>

<style lang="scss" scoped>
  #section_top {
    height: 45vh;
    background-color: #0D0F8D;

    img {
      max-height: 80%;
      margin-top: 40px;
    }
  }

  #section_bottom {
    height: 55vh;
    padding-top: 20px;
    background-color: #11093A;
  }
</style>