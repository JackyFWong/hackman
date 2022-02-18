<template>
  <div class="modal is-active">
    <div class="modal-background"></div>
    <div class="modal-content">
      <div class="card">
        <div class="card-content">
          <div class="content">
            <div v-if="win">
              <h1>You win!</h1>
            </div>
            <div v-else>
              <h1>Sorry, you lose</h1>
            </div>

            <p>Your word was {{ word }}.</p>
            <img :src="picUrl" />
          </div>
        </div>
      </div>
    </div>
    <button class="modal-close is-large" aria-label="close"></button>
  </div>
</template>

<script>
export default {
  name: "GameOver",
  props: {
    win: Boolean,
    word: String,
    picUrl: String,
  },
};
</script>

<style lang="scss"></style>
