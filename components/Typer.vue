<template>
  <div>
    <vue-typer
      :text='["Jaha, så det är dags för den här skitgasquen igen.",
      "Vad heter du?"]'
      :repeat='0'
      :shuffle='false'
      initial-action='typing'
      :pre-type-delay='500'
      :type-delay='70'
      :pre-erase-delay='500'
      :erase-delay='250'
      erase-style='clear'
      :erase-on-complete='false'
      caret-animation='blink'
      @completed='onCompleted'
    ></vue-typer>
  </div>
</template>

<script>
export default {
  methods: {
    onCompleted: function () {
      this.$emit('completed')
    }
  }
}
</script>

<style>
h1, .vue-typer {
  font-family: monospace;
}

h1 {
  margin: 1em;
}
.vue-typer .custom.char, h1 {
  color: #D4D4BD;
  background-color: #1E1E1E;
}
.vue-typer .custom.char.selected {
  background-color: #264F78;
}

.vue-typer .custom.caret {
  width: 1px;
  background-color: #3F51B5;
}
</style>
