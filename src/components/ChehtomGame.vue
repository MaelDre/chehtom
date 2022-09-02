<template>
  <h1>Welcome in Chehtom</h1>
  <displayGame ref="grille" />
  <br />
  <input id="wordInput" type="text" name="inputWord" v-model="wordToTry" v-on:keyup.enter="tryWord(wordToTry)">
  <button @click="tryWord(wordToTry)">Cheh!</button>
  <p>Essai n°{{ count }} </p>
  <p v-if="win>0"> <strong>Victory ! {{ chehWord }} !!!</strong></p>
  <p v-if="count === 6"> Perdu !</p>
  <p>Mot de {{ letternb }} lettres</p>
  <p> {{ result_message }}</p>
  <h2>La soluce pour les nullos !</h2>
  <button @click="showCheh  = !showCheh">Voir le Chehword</button>
  <p v-if="showCheh"> <strong>{{ chehword }}</strong></p>
  <button @click="resetGame">Reset Game</button>
</template>

<script>
// Sleep function
const sleep = m => new Promise(r => setTimeout(r, m))

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
        word: 'pirate',
        chehWord: 'piratecheh',
        chehList: ["pirate", "jambon", "chehhh", "chelou", "balise", "bateau", "ballon", "gateau", "cocheh", "chehbmami", "chehkira"],
        chehDict: [
          {"w": "shakira", "cw":"chehkira"},
          {"w": "crochet", "cw":"groscheh"},
          {"w": "checkup", "cw":"chehcup"},
          {"w": "attacher", "cw":"attacheh"},
          {"w": "chebmami", "cw":"chehbmami"}
        ],
        letternb: 6,
        chehWordArray: ['p','i','r','a','t','e'],
        colorArray: ["c0","c0","c0","c0","c0","c0"],
        showCheh : false,
        wordToTry : 'Un mot de 6 lettres!',
        win: 0,
        count : 0,
        resArray: ['.','.','.','.','.','.'],
        result_message : "chehh"
    }
  },
  methods: {
    async tryWord(w){
        console.log("starting tryWord method... with the word", w);
        // put the word in lower case
        w = w.toLowerCase();
        
        let rese = this.whereLetterIsInChehword('e',w);
        console.log (rese);

        let wordToTryArray = Array.from(w);
        console.log(wordToTryArray);
        
        // we check if the letters matches
        //this.checkLetter(wordToTryArray[0],0,this.word);
        //this.checkLetter(wordToTryArray[1],1,this.word);
        //this.checkLetter(wordToTryArray[2],2,this.word);
        //this.checkLetter(wordToTryArray[3],3,this.word);
        //this.checkLetter(wordToTryArray[4],4,this.word);
        //this.checkLetter(wordToTryArray[5],5,this.word);

        // New checkLetter with a loop
        for (let i=0; i < this.word.length; i++){
          this.checkLetter(wordToTryArray[i],i,this.word);
        }

        // Obsolete : useless new
        // display the word entered on the grid
        //this.$refs.grille.changeAWord(this.count,w);

        console.log("before changeAWordObj");
        // display the wordentered on the new grid Obj
        this.$refs.grille.changeAWordObj(this.count,w, this.colorArray, this.letternb);
        await sleep(4000);
        console.log("after changeAWordOb");
        

        // Ici il faudrait que je trouve un moyen d'attendre que le mot entré ait été affiché pour jouer la suite
        // Il faudrait controler l'état de l'affichage avec un genre de jeton, pour empecher toute action tant que l'affichage n'est pas fini.
        if (w === this.word) {
            console.log("victory!");
            this.win = 1;
        }
        else if ((w != this.word) && (this.count === 5)){
          // If not victory after 6 try, it is a defeat !
          this.win = -1;
          this.result_message ="Perdu Looser";
        }
        else if ((w != this.word) && (this.count < 5)){
            console.log("not finished yet ")
            this.win = 0;
            this.count++;
            //display the right letters on the grid
            this.$refs.grille.displayFirstLetter(this.count,this.word);

            // put the focus on the text input field
            wordInput.focus();
        }
    },
    whereLetterIsInChehword(l,cw){
        // renvoie l'index de la position de la lettre dans le sheh word
        // si absent : -1
        return cw.search(l);
    },
    checkLetter(l,i,cw){
        //this method checks if the letter is in the Word AND at the right place 
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
    },
    resetGame(){
        // select a new chehword
        // get random index value
        let randomIndex = Math.floor(Math.random() * this.chehDict.length);

        // get random item
        this.word = this.chehDict[randomIndex].w;

        // get the associated cheh version of the word
        this.chehWord = this.chehDict[randomIndex].cw;

        // count the number of letters
        this.letternb = this.word.length;

        // reset counter
        this.count = 0;

        // clean the grid
        this.$refs.grille.cleanGrid2(this.letternb);

        // displayFirstLetter
        this.$refs.grille.displayFirstLetter(0,this.word);
    }
  },
  mounted() {
    this.$refs.grille.displayFirstLetter(0,this.word);
    wordInput.focus();
  }
}
</script>

<style>

</style>