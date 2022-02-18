<template>
  <h1>Progress</h1>
  <div class="container is-max-desktop lettersCont">
    <div class="columns is-mobile is-centered is-vcentered">
      <div
        v-for="(letterR, index) in rightLetters"
        :key="index"
        class="column letter box"
      >
        <p>{{ letterR.toUpperCase() }}</p>
      </div>
    </div>
  </div>

  <div v-if="wrongLetters.length > 0">
    <h1>Incorrect Letters</h1>
    <div class="container is-max-desktop lettersCont">
      <div class="columns is-mobile is-centered is-vcentered">
        <div
          v-for="letterW in wrongLetters"
          :key="letterW"
          class="column letter box"
        >
          <p>{{ letterW.toUpperCase() }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Guesses",
  props: {
    wordLength: Number,
    right: Array,
    wrong: Array,
  },
  data() {
    return {
      letter: "a",
    };
  },
  computed: {
    rightLetters() {
      return this.right;
    },
    wrongLetters() {
      return this.wrong;
    },
  },
};
</script>

<style lang="scss">
.letter {
  max-width: 40px;
  height: 50px;
  margin: 0 !important;
}
.lettersCont {
  margin: 30px auto !important;
}
</style>
