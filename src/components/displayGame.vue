<template>
 <!--
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
//-->
<table>
    <tr v-for="(c, index) in chehObjArray" :key="index">
        <td v-for="(l, index) in c" :key="index" :class="c[index].color">
        {{ c[index].letter }}
        </td>
    </tr>
</table>
<p> {{ displayingstatus }}</p>
</template>

<script>
const sleep = m => new Promise(r => setTimeout(r, m))
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
            ],
            displayingstatus : false
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
            return new Promise(resolve => {
            setTimeout( function() {
                this.chehObjArray[i][j].letter = l;
                this.chehObjArray[i][j].color = col;
            }.bind(this), 1000);
            resolve('resOK');
            })
        },
        displayALetterLoop(i,j,nw,colArray, nbl){
            setTimeout(function() {   //  call a 3s setTimeout when the loop is called
                    console.log('helloo j', j);   //  your code here
                    this.chehObjArray[i][j].letter = nw[j];
                    this.chehObjArray[i][j].color = colArray[j];
                    //const res = await this.displayAletterObj(i,j, nw[j], colArray[j]);
                    
                    j++;                    //  increment the counter
                    if (j < nbl) {           //  if the counter < 10, call the loop function
                        this.displayALetterLoop(i,j,nw,colArray, nbl);             //  ..  again which will trigger another 
                    }                    //  ..  setTimeout()
                }.bind(this), 500);

        },
        async displayALetterLoop2(i,j,nw,colArray){
                const res0 = await this.displayAletterObj(i,0, nw[0], colArray[0]);
                sleep(5000);
                const res1 = await this.displayAletterObj(i,1, nw[1], colArray[1]);
                sleep(5000);
                const res2 = await this.displayAletterObj(i,2, nw[2], colArray[2]);
                sleep(5000);
                const res3 = await this.displayAletterObj(i,3, nw[3], colArray[3]);
                const res4 = await this.displayAletterObj(i,4, nw[4], colArray[4]);
                const res5 = await this.displayAletterObj(i,5, nw[5], colArray[5]);
        },

        async changeAWordObj(i,w,colArray, nbl){
            this.displayingstatus = true;
            let newWord = Array.from(w);
            console.log(newWord);
            var j=0;
            //const res = await this.displayALetterLoop(i,j,newWord,colArray);
            this.displayALetterLoop(i,j,newWord,colArray, nbl);
            //console.log("res:", res);
            this.displayingstatus = false;
            
        },
        displayFirstLetter(i,w){
            let newWord = Array.from(w);

            this.chehObjArray[i][0].letter = newWord[0];
            this.chehObjArray[i][0].color = 'c2';

            for (let j=1; j<6; j++){
                this.chehObjArray[i][j].letter = '.';
                this.chehObjArray[i][j].color = 'c0';
            }
        },
        cleanGrid(){
            this.chehObjArray= [
                [{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"}],
                [{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"}],
                [{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"}],
                [{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"}],
                [{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"}],
                [{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"}],
            ]
        },
        cleanGrid2(nbl){
            for (let i=0; i<6; i++){
                // for each line
                //this.chehObjArray[i]= [{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"}];
                for(let j=0; j<nbl; j++){
                    this.chehObjArray[i][j] = {"letter":".", "color":"c0"};
                }
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
    width: 24px;
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