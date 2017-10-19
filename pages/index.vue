<template>
  <section class="container">
    <div class="type-holder">
      <Typer v-on:completed="setCompleted" :message="typethis"/>
    </div>
    <MainInput v-if="question === 'username'"
      :inputReady="readyForInput"
      v-on:userUpdate="setUserdata"
      key="username" 
    />
    <MainInput v-else-if="question === 'fish'" 
      :inputReady="readyForInput"
      v-on:userUpdate="setUserdata"  
      key="fish" 
    />
    <MainInput v-else-if="question === 'trams'" 
      :inputReady="readyForInput" 
      v-on:userUpdate="setUserdata"
      key="trams"  
    />
    <MainInput v-else
      :inputReady="readyForInput" 
      v-on:userUpdate="setUserdata" 
      key="sista" 
    />
  </section>
</template>

<script>
import Typer from '~/components/Typer.vue'
import MainInput from '~/components/MainInput.vue'
import RockRoll from '~/assets/rickroll.js'
/* import * as firebase from 'firebase'

const firebaseApp = firebase.initializeApp({
  apiKey: 'AIzaSyB_WYmfB9wlMf5QXwiteKQvQEYmP18KkK8',
  authDomain: 'spexgasque.firebaseapp.com',
  databaseURL: 'https://spexgasque.firebaseio.com',
  projectId: 'spexgasque',
  storageBucket: '',
  messagingSenderId: '296550712740'
})
const db = firebaseApp.database() */
export default {
  components: {
    Typer,
    MainInput
  },
  data () {
    return {
      readyForInput: false,
      question: 'username',
      answer: {},
      typethis: ['skitgasque', 'vad heter du?']
    }
  },
  methods: {
    setCompleted: function () {
      console.log('tjohej completed')
      this.readyForInput = true
    },
    updateAttendantInFirebase: function (attendantName) {
      this.$firebaseRefs.attendant.push({
        name: attendantName,
        email: 'nisse@internet.com'
      })
    },
    setUserdata: function (data) {
      // Control user flow through questioins
      console.log('hej!', data)
      if (this.question === 'username') {
        this.answer.username = data.data
        this.question = 'fish'
        this.readyForInput = false
        this.typethis = ['coolt', 'vad heter din fisk?']
      } else if (this.question === 'fish') {
        this.answer.fish = data.data
        this.question = 'trams'
        this.readyForInput = false
        this.typethis = ['trams', 'vilken är din bästa sång?']
      } else if (this.question === 'trams') {
        this.question = 'sista'
        this.answer.trams = data.data
        this.readyForInput = false
        this.typethis = RockRoll
      }
    }
  }/* ,
  firebase: {
    attendant: {
      source: db.ref('/attendants'),
      asObject: true
    }
  } */
}
</script>

<style>
body {
  background-color: #1F1F1F;
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
