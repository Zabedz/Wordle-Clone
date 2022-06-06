<template>
  <div>
    <grid-component
        v-bind:word-to-guess=this.wordToGuess
        v-bind:user-guess=this.userGuess
        v-bind:current-guess=this.currentGuess

        v-bind:css-array1=this.cssArray1
        v-bind:css-array2=this.cssArray2
        v-bind:css-array3=this.cssArray3
        v-bind:css-array4=this.cssArray4
        v-bind:css-array5=this.cssArray5

        v-bind:correctAnswer=this.correctAnswer
        v-on:reset-board=resetBoard
    >
    </grid-component>
    <input-component
        v-on:guess-submitted="submitGuess">
    </input-component>
  </div>
</template>

<script>
import HeaderComponent from "@/components/HeaderComponent";
import GridComponent from "@/components/GridComponent";
import InputComponent from '@/components/InputComponent';

export default {
  name: "BoardComponent",
  data() {
    return {
      // Board constants
      currentGuess: 0,
      totalGuesses: 6,
      userGuess: '',
      correctAnswer: false,

      // Map to contain letters and cell state
      cssArray1: [],
      cssArray2: [],
      cssArray3: [],
      cssArray4: [],
      cssArray5: [],
    }
  },
  components: {GridComponent, HeaderComponent, InputComponent},
  props: {
    wordToGuess: String,
  },
  methods: {
    submitGuess(userGuess) {
      this.userGuess = userGuess
      this.setHorizontalGuess(userGuess)
    },
    setHorizontalGuess(userGuess) {
      if (this.currentGuess >= this.totalGuesses) {
        return alert("You're out of guesses.")
      }
      const letterObjectEntries = []
      for (let i = 0; i < userGuess.length; i++) {
        const letterToAdd = userGuess[i]
        let styling = 'normal'; // Doesn't exist
        if (userGuess[i] === this.wordToGuess[i]) { // Correct position
          styling = 'green'
        } else if (this.wordToGuess.includes(userGuess[i])) { // Exists but wrong position
          styling = 'yellow'
        }
        const newEntry = {
          'letter': letterToAdd,
          'styling': styling
        }
        letterObjectEntries.push(newEntry)
      }

      // Add letters and styling to props that get passed to Grid
      this.cssArray1 = [...this.cssArray1, letterObjectEntries[0]]
      this.cssArray2 = [...this.cssArray2, letterObjectEntries[1]]
      this.cssArray3 = [...this.cssArray3, letterObjectEntries[2]]
      this.cssArray4 = [...this.cssArray4, letterObjectEntries[3]]
      this.cssArray5 = [...this.cssArray5, letterObjectEntries[4]]

      this.currentGuess = this.currentGuess + 1;
      this.checkAnswer(userGuess);
    },
    checkAnswer(userGuess) {
      if (userGuess === this.wordToGuess) {
        this.correctAnswer = true;
      }
    },
    resetBoard() {
      console.log("Reset board invoked")
      this.correctAnswer = false;

      this.currentGuess = 0;
      this.totalGuesses = 6;
      this.guessLength = 5;

      this.cssArray1 = [];
      this.cssArray2 = [];
      this.cssArray3 = [];
      this.cssArray4 = [];
      this.cssArray5 = [];
    }
  }
}
</script>

<style scoped>

</style>