<template>
  <h1>CHEHHTOM</h1>
  <p>{{ letternb }} lettres à trouver</p>
  <displayGame ref="grille" />
  <br />
  <input id="wordInput" type="text" name="inputWord" v-model="wordToTry" v-on:keyup.enter="tryWord(wordToTry)">
  <br />
  <p>{{ wordToTry.length }} lettres</p>
  <br />
  <button @click="tryWord(wordToTry)" v-if="count <= 5">Cheh!</button>
  
  <h1 v-if="win>0"> <strong>Victoire ! {{result_message }} {{ chehWord }} !!!</strong></h1>
  <h1 v-if="count === 6"> Perdu ! {{result_message }} {{ chehWord }}</h1>
  <br /><br />
  <button @click="resetGame" v-if="win!=0">Recommencheh</button>

  <!-- <p>{{ count }}</p>
  <p>{{result_message }}</p> //-->
  <h1>Pour les nullos</h1>
  <p>- be removed soon-</p>
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
          {"w": "chebmami", "cw":"chehhbmami"},
          {"w": "empecher", "cw":"empechehh"},
          {"w": "toucher", "cw":"touchehhh"},
          {"w": "chenapan", "cw":"chehhnapan"},
          {"w": "cartouche", "cw":"cartouchehh"},
          {"w": "achever", "cw":"achehhhver"},

        ],
        letternb: 6,
        chehWordArray: ['p','i','r','a','t','e'],
        colorArray: ["c0","c0","c0","c0","c0","c0"],
        showCheh : false,
        wordToTry : '',
        win: 0,
        count : 0,
        resArray: ['.','.','.','.','.','.'],
        result_message : "Echehh encore"
    }
  },
  methods: {
    async tryWord(w){
      // this method  is the heart of the game
      // it is called each time the player submits a word
      
      // put the word in lower case
      w = w.toLowerCase();

      // here we should manage the accents too
      w = w.normalize("NFD").replace(/[\u0300-\u036f]/g, "");

      // convert the string to an array
      //let wordToTryArray = Array.from(w);

      // we check if the letters matches
      //for (let i=0; i < this.word.length; i++){
      //    this.checkLetter(wordToTryArray[i],i,this.word);
      //}
      this.checkWord(w);

      // display the word entered on the new grid Obj
      this.$refs.grille.changeAWordObj(this.count,w, this.colorArray, this.letternb);
      
      // we wait the word to be displayed on the grid
      await sleep(4000);
        
      // Ici il faudrait que je trouve un moyen d'attendre que le mot entré ait été affiché pour jouer la suite
      // Il faudrait controler l'état de l'affichage avec un genre de jeton, pour empecher toute action tant que l'affichage n'est pas fini.
      if (w === this.word) {
          // console.log("victory!");
          this.win = 1;
          this.result_message ="Bravoooo";
      }
      else if ((w != this.word) && (this.count === 5)){

        // If not victory after 6 try, it is a defeat !
        this.count++;
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

        // we check a letter and get its position in the cw
        let position = this.whereLetterIsInChehword(l,cw)
        if (position === i){
            console.log (l, 'est à sa place well done!');
            this.resArray[i] = l;
            this.colorArray[i] = "c2";
            // ici il faudrait retirer la lettre de rang l du mot cw
            return 2;
        }
        else if (position >= 0){
            console.log(l, "is not at the good place but in the word");
            this.colorArray[i] = "c1";
            return 1;
        }
        else{
            console.log(l, 'is not in the word');
            this.colorArray[i] = "c0";
            return 0;
        }
        console.log('colorArray:', this.colorArray);
    },
    checkWord(w){
      // This methods compares the word submited with the word to find
      // convert the string to an array

      let tempWord = this.word;
      let tempWordArray = Array.from(tempWord);
      let wordToTryArray = Array.from(w);
      let resCheckLetter = 0;

      // we check if the letters matches
      for (let i=0; i < this.word.length; i++){
          resCheckLetter = this.checkLetter(wordToTryArray[i],i,tempWord);
          console.log(resCheckLetter);

          // if the letter has been found we update the word where to search in order to avoid doublon
          // we replace the letter found by "."
          if (resCheckLetter > 0){
            tempWordArray[i] = "."
            console.log(tempWordArray);
            tempWord = tempWordArray.join("");
          }
        
      }
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

      // set win status to 0
      this.win = 0;

      // clean the grid
      this.$refs.grille.cleanGrid2(this.letternb);

      // displayFirstLetter
      this.$refs.grille.displayFirstLetter(0,this.word);
    }
  },
  mounted() {
    // this function is executed directly when the app is mounted

    this.resetGame();

    // we display the first letter of the word
    this.$refs.grille.displayFirstLetter(0,this.word);

    // we put the focus on the word text field
    wordInput.focus();
  }
}
</script>

<style>

</style>