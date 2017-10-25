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
import * as firebase from 'firebase'

const firebaseApp = firebase.initializeApp({
  apiKey: 'AIzaSyB_WYmfB9wlMf5QXwiteKQvQEYmP18KkK8',
  authDomain: 'spexgasque.firebaseapp.com',
  databaseURL: 'https://spexgasque.firebaseio.com',
  projectId: 'spexgasque',
  storageBucket: '',
  messagingSenderId: '296550712740'
})
const db = firebaseApp.database()

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
      typethis: ['Jaha', 'så var det dags för den här jävla skitgasquen igen då.', 'kul att någon orkat bry sig osv...',
        'Datumet är den 9:e December', 'Lokalen är hemlig', 'Men det är väl trevlig i alla fall.', '...', 'Som vanligt är det över och underambitiöst samtidigt i alla fall.', 'Det kommer inte vara gratis men inte heller så dyrt.', 'Klädkoden är SOMMARFIN....KLÄNNING. Inga undantag ges....(Emil)', 'När börjar gasquen? Vi vet inte. Det slumpas någon gång i November', 'Vi har dock ett antal regler', '1. Alla är sångledare (två i taget) motsols', '2. Gasquens starttid slumpas', '3. Yngsta medlemen får sitta vid ett eget barnbord', '4. Toto-recall infaller när mer än halva gasquen sjunger Totos Africa', '0. I slutet av varje gasque väljs en ny regel som gäller från och med nästa gasque.', 'Aja, nog om det.', 'Tänkte ta in lite data om er i alla fall. Det blir kul?', 'Se dock till att du fyller i anmälningskoden som ges i slutet annars kan vi inte ta in din anmälan', 'vad heter du?']
    }
  },
  methods: {
    setCompleted: function () {
      console.log('tjohej completed')
      this.readyForInput = true
    },
    updateAttendantInFirebase: function (attendantName) {
      this.$firebaseRefs.attendant.push(this.answer)
    },
    setUserdata: function (data) {
      // Control user flow through questioins
      console.log('hej!', data)
      if (this.question === 'username') {
        this.answer.username = data.data
        this.question = 'fish'
        this.readyForInput = false
        this.typethis = ['coolt', 'Någon ska ju heta det också antar jag...', 'Jag har dock alltid undrat..', 'Vad heter din fisk?']
      } else if (this.question === 'fish') {
        this.answer.fish = data.data
        this.question = 'trams'
        this.readyForInput = false
        this.typethis = ['trams.. Min fisk heter Fiske-Lina..', 'Nu har vi kommit till punkten där du skriver in din mail']
      } else if (this.question === 'trams') {
        this.question = 'sista'
        this.answer.trams = data.data
        this.readyForInput = false
        let skrivin = ['Skriv in anmälningskoden:']
        let RockPlus = RockRoll.concat(skrivin)
        this.typethis = RockPlus
      } else if (this.question === 'sista') {
        console.log(data.data)
        if (data.data !== 'rimliganmälningskod') {
          this.question = 'sista'
          let fel = ['Feeeeel svar']
          let RockPlus = fel.concat(RockRoll)
          this.typethis = RockPlus
        } else {
          this.answer.sista = data.data
          this.updateAttendantInFirebase()
          this.readyForInput = false
          this.typethis = ['tack.. Det var en bra kod. Hej då', 'Ses på gasquen', ':(              ']
        }
      }
    }
  },
  firebase: {
    attendant: {
      source: db.ref('/attendants'),
      asObject: true
    }
  }
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
