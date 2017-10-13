<template>
  <div>
    <vue-typer
      :text='["Jaha, Axel. Du verkar.. intelligent?", 
      "Men ändå så vill du bli bättre vän med Poya, Anton och Viktor?",
      "Har du ens lyssnat på något vi sagt ikväll? Antar inte det, men jag är inte chockad, när man pratar med dig så har du koncentrationen som en guldfisk." ,
      "3 sekunder in på ett samtal så är du redan på väg mot baren, som den smutsiga alkolist du är. Mannen, du har problem. Jag ska ge dig min pappas nummer efter roasten, så slipper du dricka ensam iallafall.",
      "Men oavsett om du fortsätter med dina smutsiga fasoner så gör inte det så mycket, man får ju ändå ut lika mycket av att prata dig som med sina blommor. Skillnaden är ju att dom verkar lyssna."
      ]'
      :repeat='Infinity'
      :shuffle='false'
      initial-action='typing'
      :pre-type-delay='500'
      :type-delay='70'
      :pre-erase-delay='1000'
      :erase-delay='250'
      erase-style='clear'
      :erase-on-complete='false'
      caret-animation='blink'
    ></vue-typer>
  </div>
</template>

<script>
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
  width: 10px;
  background-color: #3F51B5;
}
</style>
