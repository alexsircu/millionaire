<template> 
  <div class="answer_container toggle_class" @click="answerClicked" :data-string="answerToPass" :data-id="indexToPass">
    {{ answerToPass }}
  </div>

  <!-- qui ho testato il passaggio di dati da padre a figlio. Ho scelto di creare il contenitore della risposta come div e quindi dovevo trovare un modo per passare il contenuto del div al padre attraverso $emit, quindi ho creato un attributo personalizzato :data-string e ho inserito all'interno il contenuto della risposta, al click del div si attiva il metodo "checkIfCorrect" definito nei methods che a sua volta attiva l'strunzione $emit che crea un nuovo metodo da passare al padre e come secondo paramentro passsa il dato che gli serve, in questo caso answerToPass che ho recuperato attraverso l'istruzione event.target.getAttribute('data-string');
  E' nato poi un altro problema e mi serviva la index della risposta cliccata per gestire il cambio colore e la/il fine/continuo del gioco, quindi dentro $emit ho passato anche un altro paramentro, la index. -->
</template>

<script>
export default {
  name: "Answer",
  props: {
    answerToPass: {
      type: String,
      required: true
    },
    indexToPass: {
      type: Number,
      required: true
    }
  },
  data() {
    return {
      action: 0
    }
  },
  methods: {
    answerClicked(event) {

      const self = this;
      const answerClickedString = event.target.getAttribute('data-string');
      const answerClickedId = event.target.getAttribute('data-id');

      if (self.action == 0) {
        self.action += 1; //al primo click action = 1, al secondo click action = 2;
      } else if (self.action == 1) {
        self.action += 1; //al primo click action = 1, al secondo click action = 2;
      } else if (self.action == 2) {
        self.action = 1; //quando cambio domanda il numero di click si deve resettare
      }

      self.$emit("answerClicked", answerClickedString, answerClickedId, self.action);

      console.log(self.action);

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
    cursor: pointer;
  }
  .toggle_class:hover {
    background-color: darkgoldenrod;
  }
 
  .toggle_class::before {
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
  .toggle_class::after {
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

  .click_again::before {
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
    background-color: darkgoldenrod;
  }
  .click_again::after {
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
    background-color: darkgoldenrod;
  }

  .correct_answer::before {
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
    background-color: green;
  }
  .correct_answer::after {
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
    background-color: green;
  }

  .wrong_answer::before {
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
    background-color: red;
  }
  .wrong_answer::after {
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
    background-color: red;
  }

  .toggle_class:hover::before,
  .toggle_class:hover::after {
    background-color: darkgoldenrod;
  }

  .click_again {
    background-color: darkgoldenrod;
  }

  .correct_answer {
    background-color: green;
  }

  .wrong_answer {
    background-color: red;
  }

  .pointer_none {
    pointer-events: none;
  }
</style>