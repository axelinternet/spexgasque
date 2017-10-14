<template>
  <div class="input-holder">
    <input v-if="complete === true" autofocus></input>
  </div>
</template>

<script>
export default {

  name: 'main-input',
  props: ['complete'],
  data () {
    return {
    }
  }
}
</script>

<style>
.input-holder {
  margin: 1em;
}
.input-fake-caret {
  width: 10px;
  background-color: #3F51B5;
}

input {
  color: #D4D4BD;
  background-color: #1E1E1E;
  caret-color: #3F51B5;
  border: 0px solid blue;
  font-family: monospace;
  font-size: 1em;
  text-align: center;
  animation: fade 1s ease;
}

input:focus {
  border: 0px;
  outline: none;
}

.activeInput {  
  background-color: #264F78;
}


@keyframes fade {
  0%, 100% { background-color: #1E1E1E }
  50% { background-color: #264F78 }
}

</style>