<template>
  <div>
    <div id="section_top"> 
      <img src="../assets/millionaire.png" alt="Millionaire logo">
    </div>

    <div id="section_bottom">
      <div id="section_bottom_question">
        <Question :questionToPass="questions_array[0].question"/>
      </div>
      <div id="section_bottom_answer">
        <div class="answer_container" v-for="(answer, index) in questions_array[0].answers" :key="index">
          <Answer :answerToPass="answer" />
        </div>
      </div>
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
  },
  data() {
    return {
      questions_array: [
        {
          question: "Quale IDE è stato usato per scrivere il codice di questo gioco?",
          answers: ["A: Visual Studio Code", "B: Atom", "C: Eclipse", "D: NetBeans"],
          correct : 0
        }
      ]
    }
  },
  mounted() {
    console.log(this.questions_array[0].answers);
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
    background-color: #11093A;

    #section_bottom_question {
      padding-top: 20px;
      padding-bottom: 25px;
    }

    #section_bottom_answer {
      display: flex;
      flex-wrap: wrap;
      width: 55%;
      padding-top: 25px;
      padding-right: 35px;
      margin: auto;

      .answer_container {
        display: flex;
        justify-content: center;
        width: 50%;
        margin-bottom: 20px;
      }
    }
  }
</style>