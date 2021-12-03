<template>
  <div id="app">
    <section>
      <div class="flex flex-col justify-center items-center">
        <h1 class="title mb-14">SPLITER</h1>
        <TipCalculator />
      </div>
    </section>
  </div>
</template>

<script>
import TipCalculator from "./components/TipCalculator.vue"

export default {
  name: 'App',
  components: {
    TipCalculator
  }
}
</script>

<style>
#app {
  font-family: 'Space Mono', monospace;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  background-color: hsl(185, 41%, 84%);
  height: 100vh;
  padding: 10% 20%
}

.title {
  color :hsl(183, 100%, 15%);
  font-weight: 700;
  letter-spacing: 5px;
}
</style>
