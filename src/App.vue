<template>
    <div class="wrapper">
      <div>第{{n}}手</div>
      <div class="row">
        <Cell @click="onClickCell(0, $event)" :n="n"/>
        <Cell @click="onClickCell(1, $event)" :n="n"/>
        <Cell @click="onClickCell(2, $event)" :n="n"/>
      </div>
      <div class="row">
        <Cell @click="onClickCell(3, $event)" :n="n"/>
        <Cell @click="onClickCell(4, $event)" :n="n"/>
        <Cell @click="onClickCell(5, $event)" :n="n"/>
      </div>
      <div class="row">
        <Cell @click="onClickCell(6, $event)" :n="n"/>
        <Cell v-on:click="onClickCell(7, $event)" v-bind:n="n"/>
        <Cell v-on:click="onClickCell(8, $event)" v-bind:n="n"/>
      </div>
      <div>结果:{{result === null ? `胜负未分` : `胜方为${result}`}}</div>
    </div>
</template>
<script>
import Cell from './Cell'
  export default{
    components:{Cell},
    data(){
      return {n:0,map:[
        [null,null,null],
        [null,null,null],
        [null,null,null]
      ],result:''};
    },
    methods:{
      onClickCell(i,text){
        console.log(`${i}号被点击`);
        // console.log(this);//ok
        // this.map[2][2] = i;
        // console.log(this.map);//ok
        // i
        // 0  map[0][0]
        // 3  map[1][0]
        // 4  map[1][1]
        this.map[Math.floor(i/3)][i%3] = text
        this.n = this.n+1;
        this.tell();
      },
      tell(){
        const map = this.map;
      // let result = false
      if(map[0][0] !== null && map[0][0] === map [1][1] && map[1][1] === map [2][2]){
            this.result = map[0][0];
            // Object.freeze(this.result);
            // const this.result = map[2][2];
            return
          }
      if(map[2][0] !== null && map[0][2] === map [1][1] && map[1][1] === map [2][0]){
            this.result = map[0][2];
            return
          }
        for(let i=0;i<2;i++){
          if(map[i][0] !== null && map[i][0] === map [i][1] && map[i][1] === map[i][2]){
            this.result = map[i][0];
            return
            }
        }
        for(let j=0;j<2;j++){
          if(map[0][j] !== null && map[0][j] === map [1][j] && map[1][j] === map [2][j]){
            this.result = map[0][j];
            return
          }
        }
      }
    }
  }
</script>
<style>
.wrapper{
  position: absolute;
  top: 50%;
  left: 50%;
  margin-top: -150px;
  margin-left: -150px; 
}
.row{
  display: flex;
  flex-direction: row;
}
</style>
