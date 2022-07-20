<template>
  <h1>Welcome in Chehtom</h1>
  <displayGame ref="grille" />
  <button @click="changeSchlag"> changer le premier mot par schlag</button>
  <h2>Le jeu </h2>
  <p>Essai n°{{ count }} </p>
  <input type="text" name="inputWord" v-model="wordToTry">
  <p> le mot entré : {{ wordToTry}} </p>
  <button @click="tryWord(wordToTry)">Is it the ChehWord ?</button>
  <p v-if="win>0"> <strong>Victory</strong></p>
  <p v-if="count === 6"> Perdu !</p>
  <h2>La soluce pour les nullos !</h2>
  <button @click="showCheh  = !showCheh">Voir le Chehword</button>
  <p v-if="showCheh"> <strong>{{ chehword }}</strong></p>
</template>

<script>
import displayGame from './displayGame.vue'
export default {
  components: {
    displayGame
  },
  props: {
    msg: String
  },
  data() {
    return {
        chehword: 'pirate',
        showCheh : false,
        wordToTry : 'Un mot de 6 lettres please',
        win: 0,
        count : 0,

    }
  },
  methods: {
    tryWord(w){
        console.log("starting tryWord method... with the word", w);
        let rese = this.whereLetterIsInChehword('e',w);
        console.log (rese)
        this.$refs.grille.changeAWord(this.count,w);
        if (w === this.chehword) {
            console.log("victory!");
            this.win = 1;
        }
        else{
            this.win = 0;
            this.count++;
        }
    },
    changeSchlag(){
        this.$refs.grille.changeAWord(0,'schlag')
    },
    whereLetterIsInChehword(l,w){
        // renvoie l'index de la position de la lettre dans le sheh word
        // si absent : -1
        return w.search(l);
    }
  }
}
</script>

<style>

</style>