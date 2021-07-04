<template>
  <div id="Othello">
    <table border="2" align="center">
      <tr>
        <th width="80" bgcolor="999999">
          <font size="5">{{ showPlayer }}</font>
        </th>
        <th width="160" bgcolor="999999">
          <font size="5">{{ countTurn }}</font>
        </th>
        <th width="130" bgcolor="999999">
          <font size="5">{{ countDisk }}</font>
        </th>
      </tr>
    </table>
    <table id="table" border="0">
      <tr v-for="x in 8" v-bind:key="x.id">
        <th v-for="y in 8" v-bind:key="y.id" @click="SetDisk(x, y)">
          <tamplate v-if="area[x - 1][y - 1] == 1" id="black">{{
            disk
          }}</tamplate>
          <tamplate v-if="area[x - 1][y - 1] == 2" id="white">{{
            disk
          }}</tamplate>
          <tamplate
            v-if="decision[x - 1][y - 1] == 1 && area[x - 1][y - 1] == 0"
            id="red"
            >●</tamplate
          >
        </th>
      </tr>
    </table>
    <table bgcolor="999999"  align="center">
          <input type="button" value="reset" style="width:100;height:30" @click="reset"/>
        </table>
  </div>
</template>

<script>
export default {
  el: "#Othello",
  data() {
    return {
      area: [
        [0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 2, 1, 0, 0, 0],
        [0, 0, 0, 1, 2, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0],
      ],
      decision: [
        [0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 1, 0, 0, 0],
        [0, 0, 0, 0, 0, 1, 0, 0],
        [0, 0, 1, 0, 0, 0, 0, 0],
        [0, 0, 0, 1, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0],
      ],
      disk: "●",
      playerdisk: ["〇", "●"],
      player: 2,
      blackDisk: 2,
      whiteDisk: 2,
      round: 0,
      playerX: 0,
      playerY: 0,
      direction: 0,
      turn: 0,
      x_2nd: 0,
      y_2nd: 0,
      gameover: false,
    };
  },
  methods: {
    SetDisk: function (x, y) {
      if (this.decision[x - 1][y - 1] == 1) {
        this.area[x - 1][y - 1] = this.player;
        this.playerX = x - 1;
        this.playerY = y - 1;
        this.Decision();
        this.turnEnd();
        this.changePlayer();
        this.emptyDecision();
        if (this.emptyDecision() === true) this.changePlayer();
        this.emptyDecision();
        if (this.emptyDecision() === true) this.gameover = true;
      }
    },
    turnEnd: function () {
      this.turn += 1;
      this.blackDisk = 0;
      this.whiteDisk = 0;
      for (var x = 0; x < 8; x++) {
        for (var y = 0; y < 8; y++) {
          switch (this.area[x][y]) {
            case 1:
              this.whiteDisk += 1;
              break;
            case 2:
              this.blackDisk += 1;
              break;
          }
        }
      }
    },
    Decision: function () {
      for (this.direction = 0; this.direction < 8; this.direction++) {
        for (var other = 0; other < 8; other++) {
          switch (this.direction) {
            case 0:
              this.x_2nd = this.playerX + other;
              this.y_2nd = this.playerY;
              break;
            case 1:
              this.x_2nd = this.playerX - other;
              this.y_2nd = this.playerY;
              break;
            case 2:
              this.x_2nd = this.playerX;
              this.y_2nd = this.playerY + other;
              break;
            case 3:
              this.x_2nd = this.playerX;
              this.y_2nd = this.playerY - other;
              break;
            case 4:
              this.x_2nd = this.playerX + other;
              this.y_2nd = this.playerY + other;
              break;
            case 5:
              this.x_2nd = this.playerX + other;
              this.y_2nd = this.playerY - other;
              break;
            case 6:
              this.x_2nd = this.playerX - other;
              this.y_2nd = this.playerY + other;
              break;
            case 7:
              this.x_2nd = this.playerX - other;
              this.y_2nd = this.playerY - other;
              break;
          }
          if (
            this.x_2nd >= 0 &&
            this.x_2nd < 8 &&
            this.y_2nd >= 0 &&
            this.y_2nd < 8
          ) {
            if (
              this.area[this.x_2nd][this.y_2nd] != 0 &&
              this.area[this.x_2nd][this.y_2nd] != this.player
            ) {
              console.log('')
            } else if (
              this.area[this.x_2nd][this.y_2nd] == this.player &&
              other > 0
            ) {
              for (var changeDisk = 1; changeDisk <= other; changeDisk++) {
                switch (this.direction) {
                  case 0:
                    if (this.playerX + changeDisk < 8)
                      this.area[this.playerX + changeDisk][this.playerY] =
                        this.player;
                    break;
                  case 1:
                    if (this.playerX - changeDisk >= 0)
                      this.area[this.playerX - changeDisk][this.playerY] =
                        this.player;
                    break;
                  case 2:
                    if (this.playerY + changeDisk < 8)
                      this.area[this.playerX][this.playerY + changeDisk] =
                        this.player;
                    break;
                  case 3:
                    if (this.playerY - changeDisk >= 0)
                      this.area[this.playerX][this.playerY - changeDisk] =
                        this.player;
                    break;
                  case 4:
                    if (
                      this.playerX + changeDisk < 8 &&
                      this.playerY + changeDisk < 8
                    )
                      this.area[this.playerX + changeDisk][
                        this.playerY + changeDisk
                      ] = this.player;
                    break;
                  case 5:
                    if (
                      this.playerX + changeDisk < 8 &&
                      this.playerY - changeDisk >= 0
                    )
                      this.area[this.playerX + changeDisk][
                        this.playerY - changeDisk
                      ] = this.player;
                    break;
                  case 6:
                    if (
                      this.playerX - changeDisk >= 0 &&
                      this.playerY + changeDisk < 8
                    )
                      this.area[this.playerX - changeDisk][
                        this.playerY + changeDisk
                      ] = this.player;
                    break;
                  case 7:
                    if (
                      this.playerX - changeDisk >= 0 &&
                      this.playerY - changeDisk >= 0
                    )
                      this.area[this.playerX - changeDisk][
                        this.playerY - changeDisk
                      ] = this.player;
                    break;
                }
              }
              other = 8;
            } else if (this.area[this.x_2nd][this.y_2nd] == 0) {
              other = 8;
            }
          } else {
            other = 8;
          }
        }
      }
    },
    changePlayer: function () {
      switch (this.player) {
        case 1:
          this.player = 2;
          break;
        case 2:
          this.player = 1;
          break;
      }
      this.setDecision();
    },
    setDecision: function () {
      for (var x = 0; x < 8; x++) {
        for (var y = 0; y < 8; y++) {
          this.decision[x][y] = 0;
        }
      }
      for (x = 0; x < 8; x++) {
        for (y = 0; y < 8; y++) {
          if (this.area[x][y] == this.player) {
            for (this.direction = 0; this.direction < 8; this.direction++) {
              for (var other = 1; other < 8; other++) {
                switch (this.direction) {
                  case 0:
                    this.x_2nd = x + other;
                    this.y_2nd = y;
                    break;
                  case 1:
                    this.x_2nd = x - other;
                    this.y_2nd = y;
                    break;
                  case 2:
                    this.x_2nd = x;
                    this.y_2nd = y + other;
                    break;
                  case 3:
                    this.x_2nd = x;
                    this.y_2nd = y - other;
                    break;
                  case 4:
                    this.x_2nd = x + other;
                    this.y_2nd = y + other;
                    break;
                  case 5:
                    this.x_2nd = x + other;
                    this.y_2nd = y - other;
                    break;
                  case 6:
                    this.x_2nd = x - other;
                    this.y_2nd = y + other;
                    break;
                  case 7:
                    this.x_2nd = x - other;
                    this.y_2nd = y - other;
                    break;
                }
                if (
                  this.x_2nd < 8 &&
                  this.x_2nd >= 0 &&
                  this.y_2nd < 8 &&
                  this.y_2nd >= 0
                ) {
                  if (
                    this.area[this.x_2nd][this.y_2nd] != this.player &&
                    this.area[this.x_2nd][this.y_2nd] != 0
                  ) {
                    console.log('')
                  } else if (
                    this.area[this.x_2nd][this.y_2nd] == 0 &&
                    other > 1
                  ) {
                    this.decision[this.x_2nd][this.y_2nd] = 1;
                    other = 8;
                  } else other = 8;
                } else other = 8;
              }
            }
          }
        }
      }
    },
    reset: function () {
      this.area = [
        [0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 2, 1, 0, 0, 0],
        [0, 0, 0, 1, 2, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0],
      ];
      this.gameover = false;
      this.player = 2;
      this.turn = 0;
      this.blackDisk = 2;
      this.whiteDisk = 2;
      this.setDecision();
    },
  },
  computed: {
    emptyDecision: function () {
      for (var x = 0; x < 8; x++) {
        for (var y = 0; y < 8; y++) {
          if (this.decision[x][y] != 0) return false;
        }
      }
      return true;
    },
    showPlayer: function () {
      if (this.gameover) return "勝負あり";
      return this.playerdisk[this.player - 1] + "の番";
    },
    countTurn: function () {
      if (this.gameover) {
        if (this.blackDisk > this.whiteDisk) return "黒の勝ち";
        if (this.blackDisk < this.whiteDisk) return "白の勝ち";
        return "引き分け";
      }
      return this.turn + "ターン経過";
    },
    countDisk: function () {
      return "黒:" + this.blackDisk + "白:" + this.whiteDisk;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
input {
  font-size: 25px;
  width: 147px;
}

#status th {
  width: 100px;
  height: 20px;
  text-align: left;
}

#table th {
  width: 45px;
  height: 45px;
  font-size: 30px;
  background-color: #228833;
}

#reset {
  height: 30px;
  width: 150px;
  font-size: 20px;
}

#black {
  color: #ffffff;
  font-size: 40px;
}
#white {
  color: #000000;
  font-size: 40px;
}
#red {
  color: #ff0000;
  font-size: 40px;
}
</style>
