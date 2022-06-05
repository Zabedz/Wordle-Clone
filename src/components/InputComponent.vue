<template>
  <div class="input-group input-group-lg">
    <div class="input-group-prepend">
    </div>
    <form v-on:submit="onSubmit" class="form-control">
      <input v-model="guess"
             name="guessInput"
             type="text"
             class="form-control"
             aria-label="Sizing example input"
             aria-describedby="inputGroup-sizing-lg">
    </form>
  </div>
</template>

<script>

export default {
  name: "InputComponent",
  data() {
    return {
      guess: ''
    }
  },
  methods: {
    emitGuess(guess) {
      this.$emit('guess-submitted', guess)
    },
    onSubmit(e) {
      e.preventDefault()
      if (this.guess.length !== 5){
        alert('Only 5 letter words are allowed')
        return this.clearInput()
      }
      this.guess = this.guess.toUpperCase();
      this.emitGuess(this.guess)
      this.clearInput()
    },
    clearInput() {
      this.guess = ''
    }
  }
}
</script>

<style scoped>

</style>