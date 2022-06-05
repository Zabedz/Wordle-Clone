<template>
  <div class="container">
    <div class="row">
      <div class="col-sm">
        <ul v-for="index in currentGuess" v-bind:key="index" class="list-group">
          <li class="list-group-item" v-bind:class="getStyle(cssArray1[index - 1].styling)">
            {{ cssArray1[index - 1].letter }}
          </li>
        </ul>
      </div>
      <div class="col-sm">
        <ul v-for="index in currentGuess" v-bind:key="index" class="list-group">
          <li class="list-group-item" v-bind:class="getStyle(cssArray2[index - 1].styling)">
            {{ cssArray2[index - 1].letter }}
          </li>
        </ul>
      </div>
      <div class="col-sm">
        <ul v-for="index in currentGuess" v-bind:key="index" class="list-group">
          <li class="list-group-item" v-bind:class="getStyle(cssArray3[index - 1].styling)">
            {{ cssArray3[index - 1].letter }}
          </li>
        </ul>
      </div>
      <div class="col-sm">
        <ul v-for="index in currentGuess" v-bind:key="index" class="list-group">
          <li class="list-group-item" v-bind:class="getStyle(cssArray4[index - 1].styling)">
            {{ cssArray4[index - 1].letter }}
          </li>
        </ul>
      </div>
      <div class="col-sm">
        <ul v-for="index in currentGuess" v-bind:key="index" class="list-group">
          <li class="list-group-item" v-bind:class="getStyle(cssArray5[index - 1].styling)">
            {{ cssArray5[index - 1].letter }}
          </li>
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

    // Array of objects to contain letters and cell state
    // const arr: { name: string; salary: number }[] = [];
    cssArray1: {
      type: Array
    },
    cssArray2: {
      type: Array
    },
    cssArray3: {
      type: Array
    },
    cssArray4: {
      type: Array
    },
    cssArray5: {
      type: Array
    },

  },
  methods: {
    getStyle(condition) {
      console.log("Style condition: " , condition)
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
}

.incorrect-position {
  background-color: yellow;
}

</style>