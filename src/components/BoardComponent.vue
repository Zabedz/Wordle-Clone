<template>
  <div>
    <header-component>
    </header-component>
    <grid-component
        v-bind:word-to-guess=this.wordToGuess
        v-bind:user-guess=this.userGuess
        v-bind:current-guess=this.currentGuess

        v-bind:array1=this.array1
        v-bind:array2=this.array2
        v-bind:array3=this.array3
        v-bind:array4=this.array4
        v-bind:array5=this.array5

        v-bind:css-array1=this.cssArray1
        v-bind:css-array2=this.cssArray2
        v-bind:css-array3=this.cssArray3
        v-bind:css-array4=this.cssArray4
        v-bind:css-array5=this.cssArray5

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
      guessLength: 5,

      userGuess: '',

      // Arrays to split word
      array1: '',
      array2: '',
      array3: '',
      array4: '',
      array5: '',

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
      console.log("Word guessed in board: ", userGuess)

      this.userGuess = userGuess

      // Get the horizontal arrays


      // Set the guess variable
      this.setHorizontalGuess(userGuess)
      // this.setGuess(userGuess)
    },
    setHorizontalGuess(userGuess) {
      // Take 1 word of 5 length
      // Split its contents into 5 separate arrays into index based on current guess counter - 1
      console.log("Word to guess: ", this.wordToGuess)
      console.log("Word guessed:", userGuess)
      console.log("Current guess counter: ", this.currentGuess)

      console.log(typeof this.array1);

      // Pass into array
      this.array1 = this.array1 + userGuess[0]
      this.array2 = this.array2 + userGuess[1]
      this.array3 = this.array3 + userGuess[2]
      this.array4 = this.array4 + userGuess[3]
      this.array5 = this.array5 + userGuess[4]

      // Create new entries
      let letterObjectEntries = []
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

      //Add to cssArray
      this.cssArray1 = [...this.cssArray1, letterObjectEntries[0]]
      this.cssArray2 = [...this.cssArray2, letterObjectEntries[1]]
      this.cssArray3 = [...this.cssArray3, letterObjectEntries[2]]
      this.cssArray4 = [...this.cssArray4, letterObjectEntries[3]]
      this.cssArray5 = [...this.cssArray5, letterObjectEntries[4]]

      console.log("Printing cssArray entries:")
      console.log("css1 ", JSON.stringify(this.cssArray1));
      console.log("css2 ", JSON.stringify(this.cssArray2));
      console.log("css3 ", JSON.stringify(this.cssArray3));
      console.log("css4 ", JSON.stringify(this.cssArray4));
      console.log("css5 ", JSON.stringify(this.cssArray5));

      this.currentGuess = this.currentGuess + 1;

      this.checkAnswer(userGuess);
    },
    checkAnswer(userGuess) {
      if (userGuess === this.wordToGuess) {
        this.resetBoard()
        return alert("You got it!")
      }
    },
    resetBoard() {
      this.currentGuess = 0;
      this.totalGuesses = 6;
      this.guessLength = 5;


      this.array1 = '';
      this.array2 = '';
      this.array3 = '';
      this.array4 = '';
      this.array5 = '';
    }
  }
}
</script>

<style scoped>

</style>