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
        <div class="answer_container" v-for="(answer, index) in answersToPassArray" :key="index">
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
        },
        {
          question: "Di che materiale è fatta la punta di un giavellotto olimpico?",
          answers: ["A: resina", "B: legno", "C: metallo", "D: osso"],
          correct : 2
        },
        {
          question: "Chi è stato il primo calciatore italiano a vincere la Scarpa d'Oro, il premio che si assegna al miglior goleador del calcio europeo?",
          answers: ["A: Alessandro Del Piero", "B: Luca Toni", "C: Roberto Baggio", "D: Frncesco Totti"],
          correct : 2
        },
        {
          question: "Chi tra Pocahontas, Calamity Jane, Giovanna d'Arco e Maria Teresa d'Asburgo visse prima?",
          answers: ["A: Giovanna d'Arco", "B: Maria Teresa d'Asburgo", "C: Pocahontas", "D: Calamity Jane"],
          correct : 2
        },
        {
          question: "Dieci anni fa veniva caricata una foto che apriva la rivoluzionaria era di un nuovo social network: Instagram.Oltre a un cane, cosa ritraeva?",
          answers: ["A: un guinzaglio", "B: una mano maschile", "C: un gatto", "D: un piede femminile"],
          correct : 2
        }
      ],
      questionToPass: "",
      answersToPassArray: []
    }
  },
  mounted() {
    const self = this;

    let getRandomNumber = function(min, max) {
      return Math.round(Math.random() * (max - min) + min);
    }

    let randomNumber = getRandomNumber(0, 4);
    console.log(randomNumber);

    self.questionToPass = self.questions_array[randomNumber].question;
    self.answersToPassArray = self.questions_array[randomNumber].answers;
    
    
    // mi serve una funzione che mi genera un numero casuale
    // faccio il ciclo sull'array e prendo esattamente l'oggetto con la stessa posizione del numero casuale generato
    // inserisco la domanda dentro una variabile e l'array dentro un'altra variabile
    // passo al component della domanda solamente la domanda e al component della risposta solo l'array con le risposte
    // devo creare una funzione nei methods per gestire il click sulla risposta e il click per riprovare di nuovo 
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