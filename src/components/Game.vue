<template>
  <GameOver v-if="gameOver" :win="win" :word="word" :picUrl="picUrl" />
  <div v-if="waiting">
    <div class="columns is-centered">
      <div class="column is-one-quarter">
        <progress class="progress is-small is-primary" max="100"></progress>
      </div>
    </div>
  </div>
  <div v-else>
    <div class="container">
      <Race :player="player" />
    </div>
    <div class="container">
      <Guesses :wordLength="wordLen" :right="right" :wrong="wrong" />
    </div>
    <div class="container">
      <InputBox @submitGuess="submitGuess" />
    </div>
  </div>
</template>

<script>
import Race from "@/components/Race.vue";
import InputBox from "@/components/InputBox.vue";
import Guesses from "@/components/Guesses.vue";
import GameOver from "@/components/GameOver.vue";

export default {
  name: "Game",
  components: {
    Race,
    InputBox,
    Guesses,
    GameOver,
  },
  data() {
    return {
      word: "",
      wordLen: -1,
      picUrl: "",
      waiting: true,
      right: [],
      wrong: [],
      maxAtt: 7, // max attempts + 1 for spacing
      player: [],
      gameOver: false,
      win: false,
    };
  },
  beforeMount() {
    // 1 request per 2 seconds
    fetch("https://clemsonhackman.com/api/word?key=" + "", {
      method: "GET",
    })
      .then((resp) => resp.json())
      .then((data) => {
        this.word = data.word;
        this.wordLen = data.word.length;
        this.right = Array.from({ length: this.wordLen }, () => " ");
        console.log(this.word);
        return data.word;
      })
      .then((word) => {
        // < 100 requests per min
        fetch(
          `https://pixabay.com/api/?key=${""}` +
            `&q=${word}` +
            "&per_page=3",
          {
            method: "GET",
          }
        )
          .then((resp) => resp.json())
          .then((data) => {
            if (data.total > 0) {
              this.picUrl = data.hits[0].webformatURL;
            } else {
              this.picUrl = "@/assets/logo.png";
            }
          })
          .then((this.waiting = false));
      });
  },
  mounted() {
    // position marked by 1
    this.player = Array.from({ length: this.maxAtt }, () => 0);
    this.player[this.maxAtt - 1] = 1;
  },
  methods: {
    submitGuess(g) {
      // correct guess
      if (this.word.includes(g)) {
        for (var i = 0; i < this.wordLen; i++) {
          if (this.word.charAt(i) == g) {
            this.right[i] = g;
          }
        }
      }
      // wrong guess
      else {
        this.wrong.push(g);
        // slow player
        var pidx = this.player.indexOf(1) - 1;
        if (pidx == 0) {
          console.log("you lose")
          this.gameOver = true;
        }
        this.player[pidx] = 1;
        this.player[pidx + 1] = 0;
      }
      // check win (no more spaces)
      console.log("progress: " + this.right)
      if (!this.right.includes(" ")) {
        console.log("you win")
        this.gameOver = true;
        this.win = true;
      }
    },
  },
};
</script>

<style lang="scss">
img {
  max-height: 200px;
  width: auto;
}
</style>
