<template>
  <h3>Race</h3>
  <div class="container is-max-desktop">
    <div class="columns is-mobile is-gapless is-centered is-vcentered">
      <div class="column p-0">
        <img src="@/assets/road.png" />
      </div>
      <div class="column p-0">
        <img src="@/assets/car1-road.png" />
      </div>
      <div v-for="pos in playerTrack" :key="pos" class="column p-0">
        <img v-if="pos == 1" src="@/assets/car0-road.png" />
        <img v-else src="@/assets/road.png" />
      </div>
      <div class="column p-0">
        <img src="@/assets/road.png" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Race",
  props: {
    player: Array,
  },
  data() {
    return {};
  },
  beforeMount() {},
  mounted() {},
  computed: {
    playerTrack() {
      return this.player;
    },
  },
};
</script>

<style lang="scss">
.race {
  max-width: 100px;
  max-height: 100px;
}
</style>
