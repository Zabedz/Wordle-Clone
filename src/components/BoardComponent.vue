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
      console.log("User guess in set horizontal guess method:", userGuess)
      console.log("Current guess: ", this.currentGuess)

      console.log(typeof this.array1);

      this.array1 = this.array1 + userGuess[0]
      this.array2 = this.array2 + userGuess[1]
      this.array3 = this.array3 + userGuess[2]
      this.array4 = this.array4 + userGuess[3]
      this.array5 = this.array5 + userGuess[4]

      console.log("Printing array-string content");
      console.log(this.array1.toString());
      console.log(this.array2.toString());
      console.log(this.array3.toString());
      console.log(this.array4.toString());
      console.log(this.array5.toString());

      this.currentGuess = this.currentGuess + 1;

      for (let i = 0; i < 5; i++){
        console.log("Inside for loop to print array contents: ");
        console.log(this.array1[i])
        console.log(this.array2[i])
        console.log(this.array3[i])
        console.log(this.array4[i])
        console.log(this.array5[i])
      }
    }
  }
}
</script>

<style scoped>

</style>