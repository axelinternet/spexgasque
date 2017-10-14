<template>
  <section class="container">
    <div class="type-holder">
      <Typer v-on:completed="setCompleted"/>
    </div>
    <MainInput :complete="waitingForInput" />
  </section>
</template>

<script>
import Typer from '~/components/Typer.vue'
import MainInput from '~/components/MainInput.vue'

export default {
  components: {
    Typer,
    MainInput
  },
  data () {
    return {
      waitingForInput: false
    }
  },
  methods: {
    setCompleted: function () {
      this.waitingForInput = true
    }
  }
}
</script>

<style>
body {
  background-color: #1E1E1E;
}

.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  max-width: 90vw;
  margin: auto;
  flex-direction: column;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}

.type-holder {
  height: 2em;
  width: 100%;
}

</style>
