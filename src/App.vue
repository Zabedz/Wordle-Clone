<template>
  <div class="container">
    <header-component>
    </header-component>
    <board-component
      v-bind:wordToGuess = wordToGuess>
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
  data () {
    return {
      wordToGuess: 'Hello'.toUpperCase()
    }
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
