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
        chehWordArray: ['p','i','r','a','t','e'],
        colorArray: ["c0","c0","c0","c0","c0","c0"],
        showCheh : false,
        wordToTry : 'Un mot de 6 lettres please',
        win: 0,
        count : 0,
        resArray: ['.','.','.','.','.','.']


    }
  },
  methods: {
    tryWord(w){
        console.log("starting tryWord method... with the word", w);
        let rese = this.whereLetterIsInChehword('e',w);
        console.log (rese);

        let wordToTryArray = Array.from(w);
        console.log(wordToTryArray);
        // we check if the letters matches
        this.checkLetter(wordToTryArray[0],0,this.chehword);
        this.checkLetter(wordToTryArray[1],1,this.chehword);
        this.checkLetter(wordToTryArray[2],2,this.chehword);
        this.checkLetter(wordToTryArray[3],3,this.chehword);
        this.checkLetter(wordToTryArray[4],4,this.chehword);
        this.checkLetter(wordToTryArray[5],5,this.chehword);

        // display the word entered on the grid
        this.$refs.grille.changeAWord(this.count,w);

        // display the wordentered on the new grid Obj
        this.$refs.grille.changeAWordObj(this.count,w, this.colorArray);

        if (w === this.chehword) {
            console.log("victory!");
            this.win = 1;
        }
        else{
            this.win = 0;
            this.count++;
            //display the right letters on the grid
            this.$refs.grille.changeAWord(this.count,this.resArray.join(""));

        }
    },
    changeSchlag(){
        this.$refs.grille.changeAWord(0,'schlag')
    },
    whereLetterIsInChehword(l,cw){
        // renvoie l'index de la position de la lettre dans le sheh word
        // si absent : -1
        return cw.search(l);
    },
    checkLetter(l,i,cw){
        //this method checks if the letter is in the chehWord AND at the right place 
        if (this.whereLetterIsInChehword(l,cw) === i){
            console.log (l, 'est à sa place well done!');
            this.resArray[i] = l;
            this.colorArray[i] = "c2";
        }
        else if (this.whereLetterIsInChehword(l,cw) >= 0){
            console.log(l, "is not at the good place but in the word");
            this.colorArray[i] = "c1";
        }
        else{
            console.log(l, 'is not in the word');
            this.colorArray[i] = "c0";
        }
        console.log('colorArray:', this.colorArray);
    }
  }
}
</script>

<style>

</style>