<template>
  <div id="question_container">
    Chi è stato il primo insegnante Boolean?
  </div>
</template>

<script>
export default {
  name: "Question"
}
</script>

<style lang="scss" scoped>
  #question_container {
    position: relative;
    width: 30%;
    padding: 20px;
    border-top: 3px solid white;
    border-bottom: 3px solid white;
    margin: auto;
  }

  #question_container::before {
    position: absolute;
    left: -10%;
    top: 0;
    content: "";
    width: 100px;
    height: 100px;
    background-color: red;
  }

  #question_container::after {
    position: absolute;
    right: -10%;
    top: 0;
    content: "";
    width: 100px;
    height: 100px;
    background-color: red;
  }
</style>