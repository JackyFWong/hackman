<template>
  <h1>Your word: {{ word }}</h1>
  <img :src="picUrl" />
  <p v-if="waiting">Please wait</p>
</template>

<script>
export default {
  name: "Game",
  data() {
    return {
      word: "",
      picUrl: "",
      waiting: true,
    };
  },
  beforeMount() {
    fetch("https://clemsonhackman.com/api/word?key=" + "", {
      method: "GET",
    })
      .then((resp) => resp.json())
      .then((data) => {
        this.word = data.word;
        return data.word;
      })
      .then((word) => {
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
            }
            else {
              this.picUrl = "@/assets/logo.png";
            }
          })
          .then(this.waiting = false);
      });
  },
};
</script>

<style></style>
