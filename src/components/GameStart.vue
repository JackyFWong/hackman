<template>
  <section class="hero is-primary">
    <div class="hero-body">
      <h1 class="title">Hackman</h1>
      <p class="subtitle">
        Welcome to Hackman. You are trying to recover a priceless artifact, but
        bad guys are on your tail. Try to guess what you are holding.
      </p>
      <p>Guess right, and you will escape.</p>
    </div>
    <router-link to="/game" class="button">Let's go</router-link>
  </section>
</template>

<script>
export default {
  name: "GameStart",
};
</script>

<style lang="scss"></style>
