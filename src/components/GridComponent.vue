<template>
  <div class="container">
    <div class="row">
      <div class="col-sm">
        <ul v-for="index in currentGuess" v-bind:key="index" class="list-group">
<!--          <li class="list-group-item">{{ array1[index - 1] }}</li>-->
          <li class="list-group-item" v-bind:class="getStyle('yellow')">{{ array1[index - 1] }}</li>
        </ul>
      </div>
      <div class="col-sm">
        <ul v-for="index in currentGuess" v-bind:key="index" class="list-group">
          <li class="list-group-item">{{ array2[index - 1] }}</li>
        </ul>
      </div>
      <div class="col-sm">
        <ul v-for="index in currentGuess" v-bind:key="index" class="list-group">
          <li class="list-group-item">{{ array3[index - 1] }}</li>
        </ul>
      </div>
      <div class="col-sm">
        <ul v-for="index in currentGuess" v-bind:key="index" class="list-group">
          <li class="list-group-item">{{ array4[index - 1] }}</li>
        </ul>
      </div>
      <div class="col-sm">
        <ul v-for="index in currentGuess" v-bind:key="index" class="list-group">
          <li class="list-group-item">{{ array5[index - 1] }}</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: "GridComponent",
  data() {
    return {
      booleanValue: false
    }
  },
  props: {
    currentGuess: Number,
    wordToGuess: String,
    userGuess: String,

    // Horizontal arrays for guesses
    array1: String,
    array2: String,
    array3: String,
    array4: String,
    array5: String,

    // Contains letters and cell state
    map1: new Map(),
    map2: new Map(),
    map3: new Map(),
    map4: new Map(),
    map5: new Map(),
  },
  methods: {
    getStyle(condition) {
      switch (condition) {
        case 'yellow':
          return 'incorrect-position'
        case 'green':
          return 'correct-position'
        default:
          return ''
      }
    }
  }
}
</script>

<style scoped>

.container {

}

.col-sm {
  max-width: 500px;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
}

.list-group-item {
  margin: 0px;
  height: 50px;
}

.correct-position {
  background-color: greenyellow;
  font-size: xx-large;
}

.incorrect-position {
  background-color: yellow;
}

</style>