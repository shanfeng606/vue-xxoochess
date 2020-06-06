<template>
  <div class="wrap">
    <div>第{{n}}手</div>
    <div class="chess">
      <div class="row">
        <Cell @click="onClickCell(0,$event)" :n="n"  :con="con"/>
        <Cell @click="onClickCell(1,$event)" :n="n" :con="con"/>
        <Cell @click="onClickCell(2,$event)" :n="n" :con="con"/>
      </div>
      <div class="row">
        <Cell @click="onClickCell(3,$event)" :n="n" :con="con"/>
        <Cell @click="onClickCell(4,$event)" :n="n" :con="con"/>
        <Cell @click="onClickCell(5,$event)" :n="n" :con="con"/>
      </div>
      <div class="row">
        <Cell @click="onClickCell(6,$event)" :n="n" :con="con"/>
        <Cell @click="onClickCell(7,$event)" :n="n" :con="con"/>
        <Cell @click="onClickCell(8,$event)" :n="n" :con="con"/>
      </div>
    </div>

    <div class="result">结果：{{result === null ? '胜负未分' : `胜方为${result}`}}</div>
    <div class="reset" @click="reset">点击重置</div>
  </div>
</template>

<script>
import Cell from "./Cell";
export default {
  components: { Cell },

  data() {
    return {
      n: 0,
      map: [
        [null, null, null],
        [null, null, null],
        [null, null, null]
      ],
      result: null,
      con:true
    };
  },
  methods: {
    onClickCell(i, text) {
      // console.log(this.con)
      if(!this.con){
        return
      }


      var temp = this;
      // console.log(`${i}号被点击,内容是：${text}`);
      this.map[Math.floor(i / 3)][i % 3] = text;
      this.n = this.n + 1;
      this.tell();
      // console.log(this.map)
      //弹出提示框，通过setTimeout来实现异步，否则会堵塞
      if (this.result !== "胜负未分" && this.result !== null) {
        setTimeout(function() {
          alert(`游戏结束，胜方为${temp.result}`,);
        }, 100);
      }else if(this.n === 9 && this.result !== "胜负未分") {
        setTimeout(function() {
          alert("未分出胜负");
        }, 100);
      }
    },

    //胜负判断函数
    tell() {
      const map = this.map;
      //横
      for (let i = 0; i < 3; i++) {
        if (
          map[i][0] !== null &&
          map[i][0] === map[i][1] &&
          map[i][1] === map[i][2]
        ) {
          this.result = map[i][0];
          this.con=false;
        }
      }
      //竖
      for (let j = 0; j < 3; j++) {
        if (
          map[0][j] !== null &&
          map[0][j] === map[1][j] &&
          map[1][j] === map[2][j]
        ) {
          this.result = map[0][j];
          this.con=false;
        }
      }
      //斜
      if (
        map[0][0] !== null &&
        map[0][0] === map[1][1] &&
        map[1][1] === map[2][2]
      ) {
        this.result = map[0][0];
        this.con=false;
      }

      if (
        map[0][2] !== null &&
        map[0][2] === map[1][1] &&
        map[1][1] === map[2][0]
      ) {
        this.result = map[0][2];
        this.con=false;
      }
    },

    //重置
    reset() {
      location.reload();
    }
  }
};
</script>

<style>
.row {
  display: flex;
}
.wrap {
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
}
.result,
.reset {
  margin-top: 10px;
}
</style>
