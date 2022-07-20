<template>
<h2>La ChehGrille</h2>
 <table>
    <tr v-for="(c, index) in chehArray" :key="index">
        <td > {{ c[0] }}</td>
        <td > {{ c[1] }}</td>
        <td > {{ c[2] }}</td>
        <td > {{ c[3] }}</td>
        <td > {{ c[4] }}</td>
        <td > {{ c[5] }}</td>
    </tr>
</table>
<button @click="changeAWord(3,'blabla')">Changer un mot</button>
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
            ]
        }
    },
    methods:{
        changeAWord(i,w){
            let newWord = Array.from(w);
            console.log(newWord);
            this.chehArray[i] = newWord;
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
</style>