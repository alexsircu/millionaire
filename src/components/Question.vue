<template>
  <div id="question_container" class="one_line_content">
    {{ questionToPass }}
  </div>
</template>

<script>
export default {
  name: 'Question',
  props: {
    questionToPass: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      example : 'Chi è stato il primo insegnante Boolean?'
    }
  },
  mounted() {
    const self = this;
    const questionContainer = document.querySelector('#question_container');

    console.log(self.example.length);
    if (self.example.length > 64) {
      questionContainer.classList.remove('one_line_content');
      questionContainer.classList.add('two_line_content');
    }
  }
}
</script>

<style lang="scss" scoped>
  #question_container {
    position: relative;
    width: 30%;
    color: white;
    padding: 20px 40px;
    border-top: 3px solid white;
    border-bottom: 3px solid white;
    border-radius: 5px;
    margin: auto;
  }

  .one_line_content::before {
    position: absolute;
    left: -21px;
    top: 3.5px;
    content: "";
    width: 48px;
    height: 48px;
    transform: rotate(45deg);
    border-bottom: 3px solid white;
    border-left: 3px solid white;
    border-radius: 10px;
  }
  .one_line_content::after {
    position: absolute;
    right: -21px;
    top: 3.5px;
    content: "";
    width: 48px;
    height: 48px;
    transform: rotate(-135deg);
    border-bottom: 3px solid white;
    border-left: 3px solid white;
    border-radius: 10px;
  }

  .two_line_content::before {
    position: absolute;
    left: -26px;
    top: 6px;
    content: "";
    width: 61px;
    height: 61px;
    transform: rotate(45deg);
    border-bottom: 3px solid white;
    border-left: 3px solid white;
    border-radius: 10px;
  }
  .two_line_content::after {
    position: absolute;
    right: -26px;
    top: 6px;
    content: "";
    width: 61px;
    height: 61px;
    transform: rotate(-135deg);
    border-bottom: 3px solid white;
    border-left: 3px solid white;
    border-radius: 10px;
  }
</style>