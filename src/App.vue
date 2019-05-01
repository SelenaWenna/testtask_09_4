<template lang="pug">
  #app
    table.chessboard
      chess-header-x(:headerX="chessHeaderX")
      tr(
        v-for="j in (chessBoard.length)"
        :key="chessBoard.length - j"
        )
        chess-header-y(:headerY="chessHeaderY[chessBoard.length - j]")
        chess-cell(
          v-for="(cell, i) in chessBoard[chessBoard.length - j]"
          :key="i"
          :options="cell"
          @click="activateCell(cell.xIndex, cell.yIndex)"
          )
        chess-header-y(:headerY="chessHeaderY[chessBoard.length - j]")
      chess-header-x(:headerX="chessHeaderX")
</template>

<script>
import chessHeaderX from '@/components/chessHeaderX.vue'
import chessHeaderY from '@/components/chessHeaderY.vue'
import chessCell from '@/components/chessCell.vue'


export default {
  name: 'app',
  components: {
    chessHeaderX,
    chessHeaderY,
    chessCell
  },
  data: () => ({
    startPosition: {
      x: Infinity,
      y: Infinity
    },
    chessHeaderX: 'ABCDEFGH',
    chessHeaderY: '12345678',
  }),
  computed: {
    chessBoard() {
      const result = Array.from(this.chessHeaderX)
        .map((cellX, i) => Array.from(this.chessHeaderY).map((cellY, j) => {
        let status = ''
        if (i === this.startPosition.x && j === this.startPosition.y) {
          status = 'active'
        }
        return {
          defaultCellColor: ((i % 2) === (j % 2)) ? 'dark' : 'light',
          status,
          xIndex: i,
          yIndex: j,
        }
      }))
      let moves = this.calculateMoves()
      moves.forEach(el => {
        result[el.x][el.y].status = 'available'
      })
      return result
    }
  },
  methods: {
    validateMove(value) {
      return (value.x >= 0 && value.x <= 7) && (value.y >= 0 && value.y <= 7)
    },
    getAllMoves() {
      let delta1 = 1, delta2 = 2
      return [
        // 1
        {
          x: this.startPosition.x + delta1,
          y: this.startPosition.y + delta2
        },
        // 2
        {
          x: this.startPosition.x + delta1,
          y: this.startPosition.y - delta2
        },
        // 3
        {
          x: this.startPosition.x - delta1,
          y: this.startPosition.y + delta2
        },
        // 4
        {
          x: this.startPosition.x - delta1,
          y: this.startPosition.y - delta2
        },
        // 5
        {
          x: this.startPosition.x + delta2,
          y: this.startPosition.y + delta1
        },
        // 6
        {
          x: this.startPosition.x + delta2,
          y: this.startPosition.y - delta1
        },
        // 7
        {
          x: this.startPosition.x - delta2,
          y: this.startPosition.y + delta1
        },
        // 8
        {
          x: this.startPosition.x - delta2,
          y: this.startPosition.y - delta1
        }
      ]
    },
    calculateMoves() {
      return this.getAllMoves().filter((el) => this.validateMove(el))
    },
    activateCell(xIndex, yIndex) {
      this.$set(this.startPosition, 'x', xIndex)
      this.$set(this.startPosition, 'y', yIndex)
    }
  },
}
</script>

<style scoped>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.chessboard {
  border: 1px solid grey;
  width: 470px;
  margin: 0 auto;
  border-collapse: collapse;
}
</style>
