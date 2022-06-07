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
    >
    </grid-component>
    <input-component
        v-on:guess-submitted="submitGuess"
        v-bind:disabled=correctAnswer>
    </input-component>
    <reset-game-button-component
        v-bind:show-button=this.correctAnswer
        v-on:reset-game="resetBoard">
    </reset-game-button-component>
  </div>
</template>

<script>
import HeaderComponent from "@/components/HeaderComponent";
import GridComponent from "@/components/GridComponent";
import InputComponent from '@/components/InputComponent';
import ResetGameComponent from "@/components/ResetGameComponent";

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
  components: {ResetGameButtonComponent: ResetGameComponent, GridComponent, HeaderComponent, InputComponent},
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
      const letterObjectEntries = this.setArrays(userGuess);

      // Add letters and styling to props that get passed to Grid
      this.cssArray1 = [...this.cssArray1, letterObjectEntries[0]]
      this.cssArray2 = [...this.cssArray2, letterObjectEntries[1]]
      this.cssArray3 = [...this.cssArray3, letterObjectEntries[2]]
      this.cssArray4 = [...this.cssArray4, letterObjectEntries[3]]
      this.cssArray5 = [...this.cssArray5, letterObjectEntries[4]]

      this.currentGuess = this.currentGuess + 1;
      this.checkAnswer(userGuess);
    },
    async checkAnswer(userGuess) {
      if (userGuess === this.wordToGuess) {
        this.correctAnswer = true;
        this.getNewWord();
      }
    },
    getLetterCount(userGuess) {
      let countObject = {};
      for (let char of userGuess) {
        if (!countObject[char] && char !== ' ') {
          countObject[char] = 1;
        } else if (char !== ' ') {
          countObject[char] = countObject[char] + 1;
        }
      }
      return countObject;
    },
    setArrays(userGuess) {
      let letterCountSet = this.getLetterCount(this.wordToGuess);
      const letterObjectEntries = []

      for (let i = 0; i < userGuess.length; i++) {
        const letterToAdd = userGuess[i] // == H

        let styling = 'normal'; // Doesn't exist
        if (letterToAdd === this.wordToGuess[i]) { // Correct position

          if (letterCountSet[`${letterToAdd}`] > 0) {
            styling = 'green'
            letterCountSet[`${letterToAdd}`] = letterCountSet[`${letterToAdd}`] - 1;
          }
        } else if (this.wordToGuess.includes(letterToAdd)) { // Exists but wrong position
          if (letterCountSet[`${letterToAdd}`] > 0) {
            styling = 'yellow'
            letterCountSet[`${letterToAdd}`] = letterCountSet[`${letterToAdd}`] - 1;
          }
        }
        const newEntry = {
          'letter': letterToAdd,
          'styling': styling
        }
        letterObjectEntries.push(newEntry)
      }
      return letterObjectEntries;
    },
    resetBoard() {
      this.correctAnswer = false;

      this.currentGuess = 0;
      this.totalGuesses = 6;
      this.guessLength = 5;

      this.cssArray1 = [];
      this.cssArray2 = [];
      this.cssArray3 = [];
      this.cssArray4 = [];
      this.cssArray5 = [];
    },
    getNewWord() {
      this.$emit('get-word');
    },
  }
}
</script>

<style scoped>

</style>