<template>
  <div id="app">
    <div class="container">
      <template v-for="item in numOfSW">
        <Stopwatch />
      </template>
      <AddButton @addStopwatch="addStopwatch"/>
    </div>
  </div>
</template>

<script>

import Stopwatch from "./components/Stopwatch";
import AddButton from "./components/AddButton";
export default {
  name: 'App',
  components: {
    AddButton,
    Stopwatch
  },
  data: () => ({
    numOfSW: 3
  }),
  methods: {
    addStopwatch() {
      this.numOfSW ++;
    }
  }
}
</script>

<style lang="scss">

  @font-face {
    font-family: 'Gotham Pro Regular';
    src: url('./fonts/gotham_pro/GothamPro.eot');
    src: url('./fonts/gotham_pro/GothamPro.eot?#iefix') format('embedded-opentype'),
    url('./fonts/gotham_pro/GothamPro.woff') format('woff'),
    url('./fonts/gotham_pro/GothamPro.ttf') format('truetype');
    font-weight: normal;
    font-style: normal;
  }

  body {
    background-color: #353638;
  }
  button {
    width: 20px;
    height: 20px;
    position: relative;
    background-color: transparent;
    border: none;
    &:focus {
      outline: none;
    }
  }
  #app {
    margin-top: 72px;
    margin-bottom: 72px;
    font-family: "Gotham Pro Regular", sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;

  }
  .container {
    width: 1024px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: repeat(auto-fit, 225px);
    grid-gap: 50px;
    justify-content: center;
  }
  
  @media (max-width: 1023px) {
    .container {
        width: 700px;
    }
  }
  @media (max-width: 768px) {
    .container {
      width: 600px;
    }
  }
  @media (max-width: 650px) {
    .container {
      width: 400px;
    }
  }


</style>
