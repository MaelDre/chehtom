<template>
<h2>La ChehGrille</h2>
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
                [{"letter":"a", "color":"c2"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"}],
                [{"letter":"b", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"}],
                [{"letter":"b", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"}],
                [{"letter":"b", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"}],
                [{"letter":"b", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"}],
                [{"letter":"b", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"},{"letter":".", "color":"c0"}],
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
        changeAWordObj(i,w,colArray){
            let newWord = Array.from(w);
            console.log(newWord);

            this.chehObjArray[i][0].letter = newWord[0];
            this.chehObjArray[i][1].letter = newWord[1];
            this.chehObjArray[i][2].letter = newWord[2];
            this.chehObjArray[i][3].letter = newWord[3];
            this.chehObjArray[i][4].letter = newWord[4];
            this.chehObjArray[i][5].letter = newWord[5];

            this.chehObjArray[i][0].color = colArray[0];
            this.chehObjArray[i][1].color = colArray[1];
            this.chehObjArray[i][2].color = colArray[2];
            this.chehObjArray[i][3].color = colArray[3];
            this.chehObjArray[i][4].color = colArray[4];
            this.chehObjArray[i][5].color = colArray[5];
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
  color: #DD00FF;
}
.c2 {
  color: #44AA38;
}
.maclasse2{
    font-size:40px;
    color: #44AA38;
}
</style>