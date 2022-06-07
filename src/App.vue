<template>
  <div class="container">
    <header-component>
    </header-component>
    <board-component
        v-bind:wordToGuess=wordToGuess
        v-on:get-word="getWord">
    </board-component>
    <footer-component>
    </footer-component>
  </div>
</template>

<script>
import BoardComponent from "@/components/BoardComponent";
import HeaderComponent from "@/components/HeaderComponent";
import FooterComponent from "@/components/FooterComponent";

export default {
  name: 'App',
  components: {
    BoardComponent,
    HeaderComponent,
    FooterComponent
  },
  data() {
    return {
      wordToGuess: ''
    }
  },
  methods: {
    async getWord() {
      const endPoint = "https://random-word-api.herokuapp.com/word?length=5";
      const res = await fetch(endPoint);
      const word = await res.json();

      this.wordToGuess = word[0].toUpperCase();
    },
  },
  created () {
    this.wordToGuess = 'HELLO';
    // this.getWord();
  }
}
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

.container {
  padding: 20px;
}
</style>
