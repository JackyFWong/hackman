<template>
  <div class="container is-max-desktop">
    <form @submit.prevent="$emit('submitGuess', guess.toLowerCase()); guess=''">
      <input class="input is-large mr-1" type="text" maxlength="1" size="1" 
      required v-model="guess" />
      <input class="button is-primary is-large ml-1" type="submit" value="Submit" />
    </form>
  </div>
</template>

<script>
export default {
  name: "InputBox",
  data() {
    return {
      guess: "",
    };
  },
};
</script>

<style lang="scss">
input {
  width: auto !important;
  text-align: center;
}
</style>
