<template>
  <div class="input-group input-group-lg">
    <div class="input-group-prepend">
    </div>
    <form v-on:submit="onSubmit" class="form-control">
      <input v-model="userGuess"
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
      userGuess: '',
      guessLength : 5
    }
  },
  methods: {
    emitGuess(guess) {
      this.$emit('guess-submitted', guess)
    },
    onSubmit(e) {
      e.preventDefault()
      if (this.userGuess.length !== this.guessLength){
        alert('Only 5 letter words are allowed')
        return this.clearInput()
      }
      this.userGuess = this.userGuess.toUpperCase();
      this.emitGuess(this.userGuess)
      this.clearInput()
    },
    clearInput() {
      this.userGuess = ''
    }
  }
}
</script>

<style scoped>

</style>