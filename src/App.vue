<template>
  <div id="#app">
    <div class="pTest">
      Добредојдовте на ClickMaster играта, во оваа игра, во различни интервали,
      на екранот ќе се појави квадрат, целта е да се кликне на квадратот што е
      можно побрзо! Брзината на реакција ќе ја одреди гејмерската можност на
      играчите.
    </div>

    <button
      v-show="!showPlayAgain"
      @click="funkcija()"
      :disabled="buttonDisabled"
    >
      Стисни да ја играш играта
    </button>
    <button v-show="showPlayAgain" @click="funkcija()">Играј повторно</button>
    <BlockVue
      :showBlock="showBlock"
      :vremePristignuvanje="vremePristignuvanje"
      @bananica="povratBlock"
    ></BlockVue>

    <ResultsVue
      :razlika="razlika"
      :prikaziRezultati="prikaziRezultati"
    ></ResultsVue>
  </div>
</template>

<script>
import BlockVue from "./components/BlockVue.vue";
import ResultsVue from "./components/ResultsVue.vue";

export default {
  name: "App",
  components: {
    BlockVue,
    ResultsVue,
  },
  methods: {
    funkcija() {
      this.prikaziRezultati = "";
      this.buttonDisabled = true;

      const randomNumber = Math.random() * 2;
      setTimeout(() => {
        this.showBlock = true;
        this.vremePristignuvanje = Date.now();
      }, randomNumber * 1000);
    },
    povratBlock(value) {
      this.prikaziRezultati = value[0];
      this.vremeStisok = value[1];
      this.razlika = (this.vremeStisok - this.vremePristignuvanje) / 1000;
      this.showBlock = false;
      this.showPlayAgain = true;
    },
  },

  data() {
    return {
      showBlock: false,
      vremePristignuvanje: "",
      prikaziRezultati: "",
      vremeStisok: "",
      razlika: "",
      buttonDisabled: false,
      showPlayAgain: false,
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.pTest {
  display: flex;
  justify-items: center;
  align-items: center;
  color: rgb(208, 208, 152);
  width: 300px;
  font-size: 12px;
  margin: auto;
  margin-bottom: 20px;
}
</style>
