<template>
  <div v-bind:class="{'is-active': showModal }" class="modal">
    <div class="modal-background"></div>
    <div class="modal-content">
      <div class="card">
        <div class="card-content">
          <div class="content">
            <div v-if="win">
              <h1>You win!</h1>
              <p>You managed to get away. Great job.</p>
              <p>
                You managed to recover:
                <span class="has-text-weight-medium">{{ word }}</span
                >.
              </p>
            </div>
            <div v-else>
              <h1>Sorry, you lose</h1>
              <p>Unfortunately, the bad guys caught up.</p>
              <p>
                They took your:
                <span class="has-text-weight-medium">{{ word }}</span
                >.
              </p>
            </div>

            <div class="box">
              <img :src="picUrl" />
            </div>
          </div>
        </div>
      </div>
    </div>
    <button class="modal-close is-large" @click="offModal"></button>
  </div>
</template>

<script>
export default {
  name: "GameOver",
  props: {
    win: Boolean,
    word: String,
    picUrl: String,
    showModal: Boolean,
  },
};
</script>

<style lang="scss"></style>
