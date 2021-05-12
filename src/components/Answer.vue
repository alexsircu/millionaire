<template>
  <div> 
    <div class="answer_container" @click="answerClicked" :data-value="answerToPass">{{ answerToPass }}</div>
  </div>

  <!-- qui ho testato il passaggio di dati da padre a figlio. Ho scelto di creare il contenitore della risposta come div e quindi dovevo trovare un modo per passare il contenuto del div al padre attraverso $emit, quindi ho creato un attributo personalizzato :data-value e ho inserito all'interno il contenuto della risposta, al click del div si attiva il metodo "checkIfCorrect" definito nei methods che a sua volta attiva l'strunzione $emit che crea un nuovo metodo da passare al padre e come secondo paramentro passsa il dato che gli serve, in questo caso answerToPass che ho recuperato attraverso l'istruzione event.target.getAttribute('data-value'); -->
</template>

<script>
export default {
  name: "Answer",
  props: {
    answerToPass: {
      type: String,
      required: true
    }
  },
  methods: {
    answerClicked(event) {

      const self = this;
      const answerClickedString = event.target.getAttribute('data-value');
      self.$emit("answerClicked", answerClickedString);

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