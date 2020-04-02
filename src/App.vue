<template>
  <div class="wrapper">
    <div class="ox">井 字 棋</div>
    <div>第{{n}}步</div>
    <div class="chess">
      <div class="row">
        <Cell @click="onClickCell(0, $event)" :n="n" />
        <Cell @click="onClickCell(1, $event)" :n="n" />
        <Cell @click="onClickCell(2, $event)" :n="n" />
      </div>
      <div class="row">
        <Cell @click="onClickCell(3, $event)" :n="n" />
        <Cell @click="onClickCell(4, $event)" :n="n" />
        <Cell @click="onClickCell(5, $event)" :n="n" />
      </div>
      <div class="row">
        <Cell @click="onClickCell(6, $event)" :n="n" />
        <Cell @click="onClickCell(7, $event)" :n="n" />
        <Cell @click="onClickCell(8, $event)" :n="n" />
      </div>
    </div>
    <br>
    <div>
      {{result===null?'胜负未分':`胜方为${result}`}}
    </div>
  </div>
</template>


<script>
  import Cell from "./Cell"
  export default {
    components: {
      Cell
    },
    data() {
      return {
        n: 0,
        map: [
          [null, null, null],
          [null, null, null],
          [null, null, null]
        ],
        result: null
      }
    },
    methods: {
      onClickCell(i, text) {
        console.log(`${i}号,内容是:${text}`)
        this.map[Math.floor(i / 3)][i % 3] = text
        if (this.n < 9) {
          this.n += 1
        } else {
          return this.n
        }
        this.tell()
      },
      tell() {
        const map = this.map
        for (let i = 0; i < 2; i++) {
          if (map[i][0] !== null &&
            map[i][0] === map[i][1] &&
            map[i][1] === map[i][2]
          ) {
            this.result = map[i][0]
          }
        }
        for (let s = 0; s < 2; s++) {
          if (map[0][s] !== null &&
            map[0][s] === map[1][s] &&
            map[1][s] === map[2][s]
          ) {
            this.result = map[0][s]
          }
        }
        if (map[0][0] !== null &&
          map[0][0] === map[1][1] &&
          map[1][1] === map[2][2]
        ) {
          this.result = map[0][0]
        }
        if (map[0][2] !== null &&
          map[0][2] === map[1][1] &&
          map[1][1] === map[2][0]
        ) {
          this.result = map[0][2]
        }
      }
    }
  }
</script>

<style>
  .ox{
    font-size: 30px;
    font-weight: bold;
  }
  .row {
    display: flex;
  }
  .wrapper{
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  }
</style>