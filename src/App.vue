<template>
  <div class="container">
    <board-component
      v-bind:wordToGuess = wordToGuess
    >
    </board-component>
  </div>
</template>

<script>
import BoardComponent from "@/components/BoardComponent";
import InputComponent from "@/components/InputComponent";

export default {
  name: 'App',
  components: {
    InputComponent,
    BoardComponent,
  },
  data () {
    return {
      wordToGuess: 'Hello'
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
