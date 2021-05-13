<template>
  <div>
    <div id="section_top"> 
      <img src="../assets/millionaire.png" alt="Millionaire logo">
    </div>

    <div id="section_bottom">
      <div id="section_bottom_question">
        <Question :questionToPass="questionToPass"/>
      </div>
      <div id="section_bottom_answer">
        <div class="answer_container_parent" v-for="(answer, index) in answersToPassArray" :key="index">
          <Answer :answerToPass="answer" :indexToPass="index" @answerClicked="checkIfCorrect" />
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
      questionsArray: [
        {
          question: "Quale IDE è stato usato per scrivere il codice di questo gioco?",
          answers: ["A: Visual Studio Code", "B: Atom", "C: Eclipse", "D: NetBeans"],
          correct : 0
        },
        {
          question: "Di che materiale è fatta la punta di un giavellotto olimpico?",
          answers: ["A: Resina", "B: Legno", "C: Metallo", "D: Osso"],
          correct : 2
        },
        {
          question: "Chi è stato il primo calciatore italiano a vincere la Scarpa d'Oro, il premio che si assegna al miglior goleador del calcio europeo?",
          answers: ["A: Alessandro Del Piero", "B: Luca Toni", "C: Roberto Baggio", "D: Francesco Totti"],
          correct : 1
        },
        {
          question: "Chi tra Pocahontas, Calamity Jane, Giovanna d'Arco e Maria Teresa d'Asburgo visse prima?",
          answers: ["A: Giovanna d'Arco", "B: Maria Teresa d'Asburgo", "C: Pocahontas", "D: Calamity Jane"],
          correct : 0
        },
        {
          question: "Dieci anni fa veniva caricata una foto che apriva la rivoluzionaria era di un nuovo social network: Instagram.Oltre a un cane, cosa ritraeva?",
          answers: ["A: Un guinzaglio", "B: Una mano maschile", "C: Un gatto", "D: Un piede femminile"],
          correct : 3
        }
      ],
      questionToPass: "",
      answersToPassArray: [],
      randomNumberGenerated: null
    }
  },
  mounted() {

    this.questionCreation(); // funzione che mi permette di creare la domanda e le risposte
    
  },
  methods: {
    checkIfCorrect(string, id) {

      const self = this;
      const correctAnswerNumber = self.questionsArray[self.randomNumberGenerated].correct;
      const answersContainer = document.querySelectorAll('.answer_container');

      if (string === self.questionsArray[self.randomNumberGenerated].answers[correctAnswerNumber]) {

        // in caso di risposta corretta
        answersContainer[correctAnswerNumber].classList.add("correct_answer");
        answersContainer[correctAnswerNumber].classList.remove("toggle_class");

        setTimeout(self.questionCreation, 1000); // il gioco deve fare un'altra domanda e andare avanti

        // modifico tutte le classi altrimenti rimarrebbero verdi/rosse
        if (self.questionCreation) {

          answersContainer[correctAnswerNumber].classList.remove("correct_answer");
          answersContainer[correctAnswerNumber].classList.add("toggle_class");
          
          answersContainer.forEach(element => {

            element.classList.remove("wrong_answer");
            element.classList.add("toggle_class");

          });  

        }

      } else {
        
        // in caso di risposta sbagliata
        for (let i = 0; i < answersContainer.length; i++) {

          if (id == i) {

            answersContainer[i].classList.add("wrong_answer");
            answersContainer[i].classList.remove("toggle_class");
          
          } 
        }
      }

    },
    questionCreation() {

      const self = this;
      self.randomNumberGenerated = null; //lo devo svuotare ogni volta che deve essere creata una nuova domanda
      const arrayLength = self.questionsArray.length - 1; //lunghezza array per sapere quanti numeri generare random
      let randomNumber = self.getRandomNumber(0, arrayLength);
      console.log(randomNumber);

      self.questionToPass = self.questionsArray[randomNumber].question;
      self.answersToPassArray = self.questionsArray[randomNumber].answers;

      self.randomNumberGenerated = randomNumber;

    },
    getRandomNumber(min, max) {

      return Math.round(Math.random() * (max - min) + min);

    }
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

      .answer_container_parent {
        display: flex;
        justify-content: center;
        width: 50%;
        margin-bottom: 20px;
      }
    }
  }
</style>