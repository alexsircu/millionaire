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
      <template v-if="buttonText.length > 0">
        <div id="section_bottom_button">
        <Button :buttonTextToPass="buttonText" @buttonClicked="questionCreationAfterCheck"/>
      </div>
      </template>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Question from "./Question.vue";
import Answer from "./Answer.vue";
import Button from "./Button.vue";

export default {
  name: "Container",
  components: {
    Question,
    Answer,
    Button
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
      randomNumberGenerated: null,
      buttonText: "",
      score: 0
    }
  },
  mounted() {

    this.questionCreationInMounted(); // funzione che mi permette di creare la domanda e le risposte
    
  },
  methods: {
    checkIfCorrect(string, id, action) {

      const self = this;
      const correctAnswerNumber = self.questionsArray[self.randomNumberGenerated].correct;
      const answersContainer = document.querySelectorAll('.answer_container');

      if (action == 1) {
        //primo click viene selezionata la risposta
        
        for (let i = 0; i < answersContainer.length; i++) {
          if (id == i) {
            answersContainer[i].classList.add("click_again");
            answersContainer[i].classList.remove("toggle_class");  
          } 
        }
      
      } else if (action == 2) {
        //secondo click c'è il controllo se la domanda è corretta oppure no

        if (string === self.questionsArray[self.randomNumberGenerated].answers[correctAnswerNumber]) {
          // in caso di risposta corretta
          answersContainer[correctAnswerNumber].classList.add("correct_answer");
          answersContainer[correctAnswerNumber].classList.remove("toggle_class");

          self.buttonText = "Prossima domanda";
          self.score++;

        } else {
          // in caso di risposta sbagliata
          for (let i = 0; i < answersContainer.length; i++) {
            if (id == i) {
              answersContainer[i].classList.add("wrong_answer");
              answersContainer[i].classList.remove("toggle_class");
            } 
          }
          self.buttonText = "Fine gioco";
        }
        //appena ho fatto entrambi i click non posso più cliccare sulle risposte
        answersContainer.forEach(element => {
          element.classList.add("pointer_none");  
        });
      }
    },
    questionCreationInMounted() {

      const self = this;
      self.randomNumberGenerated = null; //lo devo svuotare ogni volta che deve essere creata una nuova domanda
      const arrayLength = self.questionsArray.length - 1; //lunghezza array per sapere quanti numeri generare random
      let randomNumber = self.getRandomNumber(0, arrayLength);
      console.log(randomNumber);

      self.questionToPass = self.questionsArray[randomNumber].question;
      self.answersToPassArray = self.questionsArray[randomNumber].answers;
      self.randomNumberGenerated = randomNumber;

    },
    questionCreationAfterCheck() {

      //funzione che mi permette di andare avanti con il gioco se la risposta è corretta
      const self = this;
      const correctAnswerNumber = self.questionsArray[self.randomNumberGenerated].correct;
      const answersContainer = document.querySelectorAll('.answer_container');
      const questionContainer = document.querySelector('#question_container');
  
      if (self.buttonText === 'Prossima domanda') {
        self.questionCreationInMounted();

        if (self.questionToPass.length > 64) {
          questionContainer.classList.remove('one_line_content');
          questionContainer.classList.add('two_line_content');
        } else {
          questionContainer.classList.add('one_line_content');
          questionContainer.classList.remove('two_line_content');
        } //cambiamento dimensioni del contenitore della domanda

        answersContainer[correctAnswerNumber].classList.remove("correct_answer");
        answersContainer[correctAnswerNumber].classList.add("toggle_class");

        answersContainer.forEach(element => {
          element.classList.remove("wrong_answer");
          element.classList.remove("click_again");
          element.classList.remove("pointer_none");
          element.classList.add("toggle_class");
        });
        
        self.buttonText = "";
      } else if (self.buttonText === 'Fine gioco') {
        console.log("Il tuo punteggio totale è:" + self.score);
      }
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

    #section_bottom_button {
      width: 44.5%;
      text-align: center;
      margin: auto;
    }
  }
</style>