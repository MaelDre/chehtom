<template>
 <table>
    <tr v-for="(c, index) in chehObjArray" :key="index">
        <td :class="c[0].color"> {{ c[0].letter }}</td>
        <td :class="c[1].color"> {{ c[1].letter }}</td>
        <td :class="c[2].color"> {{ c[2].letter }}</td>
        <td :class="c[3].color"> {{ c[3].letter }}</td>
        <td :class="c[4].color"> {{ c[4].letter }}</td>
        <td :class="c[5].color"> {{ c[5].letter }}</td>
    </tr>
</table>
</template>

<script>
export default {
    data(){
        return{
            displayedWord: "bonjour",
            wordArray: ['b','o','n','j','o','u'],
            chehArray :[
                ['b','.','.','.','.','.'],
                ['c','.','.','.','.','.'],
                ['d','.','.','.','.','.'],
                ['e','.','.','.','.','.'],
                ['f','.','.','.','.','.'],
                ['g','.','.','.','.','.']
            ],
            chehColorArray :[
                [0,0,0,0,0,0],
                [0,0,0,0,0,0],
                [0,0,0,0,0,0],
                [0,0,0,0,0,0],
                [0,0,0,0,0,0],
                [0,0,0,0,0,0]
            ],
            chehObjArray: [
                [{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"}],
                [{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"}],
                [{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"}],
                [{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"}],
                [{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"}],
                [{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"}],
            ]
        }
    },
    methods:{
        changeAWord(i,w){
            let newWord = Array.from(w);
            console.log(newWord);
            this.chehArray[i] = newWord;
        },
        changeAWordCol(i,w,colArray){
            let newWord = Array.from(w);
            console.log(newWord);


            this.chehArray[i][0] = newWord[0];
            this.chehArray[i][1] = newWord[1];
            this.chehArray[i][2] = newWord[2];
            this.chehArray[i][3] = newWord[3];
            this.chehArray[i][4] = newWord[4];
            this.chehArray[i][5] = newWord[5];
        },
        displayAletterObj(i,j,l,col){
                this.chehObjArray[i][j].letter = l;
                this.chehObjArray[i][j].color = col;
        },
        displayALetterLoop(i,j,nw,colArray){
            setTimeout(function() {   //  call a 3s setTimeout when the loop is called
                    console.log('helloo j', j);   //  your code here
                    this.chehObjArray[i][j].letter = nw[j];
                    this.chehObjArray[i][j].color = colArray[j];
                    j++;                    //  increment the counter
                    if (j < 6) {           //  if the counter < 10, call the loop function
                        this.displayALetterLoop(i,j,nw,colArray);             //  ..  again which will trigger another 
                    }                       //  ..  setTimeout()
                }.bind(this), 1000);
        },
        changeAWordObj(i,w,colArray){
            let newWord = Array.from(w);
            console.log(newWord);
            var j=0;
            this.displayALetterLoop(i,j,newWord,colArray);
        },
        displayFirstLetter(i,w){
            let newWord = Array.from(w);

            this.chehObjArray[i][0].letter = newWord[0];
            this.chehObjArray[i][0].color = 'c2';

            for (let j=1; j<6; j++){
                this.chehObjArray[i][j].letter = '.';
                this.chehObjArray[i][j].color = 'c0';
            }
        }
    }
}
</script>

<style>
table{
    font-size:28px;
    margin-left: auto;
    margin-right: auto;
}
td { 
    border-width:1px;
    border-style:solid; 
    border-color:black;
}
.c0 {
  color: #883838;
}
.c1 {
  color: #000000;
  background-color: rgb(255, 255, 0);
}
.c2 {
  color: #000000;
  background-color: #44AA38;
}
.maclasse2{
    font-size:40px;
    color: #44AA38;
}
</style>