<template>
  <div id="Slime">
    <table border="0" align="center">
      <tr>
        <th>{{ cha[0].name }}</th>
      </tr>
      <tr>
        <th>HP:{{ cha[0].hp }}</th>
      </tr>
    </table>
    <table border="1" width="180" align="center">
      <tr>
        <th><p1>slime</p1><br /></th>
      </tr>
      <tr>
        <th>
          <p1>HP:</p1
          ><p1 v-for="i in Math.floor((cha[1].hp + 4) / 5)" v-bind:key="i.id"
            >=</p1
          ><br /><br />
          <p1>^</p1><br />
          <p1 v-if="cha[1].hp > 0">(0  0)</p1
          ><p1 v-if="cha[1].hp <= 0">(x  x)</p1><br /><br />
        </th>
      </tr>
    </table>
    <table border="0" align="center">
    <button
      @click="
        attack(0, 1);
        attack(1, 0);
      "
    >
      攻撃
    </button>
    <button
      @click="
        spell(0, 1);
        attack(1, 0);
      "
    >
      呪文
    </button>
    <button
      @click="
        use_herb(0);
        attack(1, 0);
      "
    >
      薬草({{ herb }})
    </button>
    </table>
    <table border="0" align="center">
    バトルメッセージ:
    </table>
    <div class="scroll_bar">
      <p1 v-for="i in battle_massage.length" v-bind:key="i.id"
        >{{ battle_massage[i - 1] }}<br
      /></p1>
    </div>
  </div>
</template>
<script>
var cha = [
  {
    name: "村の英雄",
    hp: 20,
    hp_Maximus: 20,
    atk: 18,
    def: 15,
  },
  {
    name: "スライム",
    hp: 35,
    atk: 15,
    def: 40,
  },
];
export default {
  el: "Slime",
  data() {
    return {
      cha: cha,
      damage: 0,
      battle_massage: [""],
      massage_number: 0,
      herb: 3,
    };
  },
  methods: {
    attack: function (attacker, pasive) {
      if (cha[attacker].hp > 0 && cha[pasive].hp > 0) {
        if (cha[pasive].hp > 0) {
          this.damage = Math.floor(
            cha[attacker].atk / 2 - cha[pasive].def / 4 + Math.random() * 1
          );
          if (this.damage <= 0) this.damage = 1;
          cha[pasive].hp -= Math.floor(this.damage);
          this.battle_massage[this.massage_number] =
            cha[attacker].name + "の攻撃!";
          this.massage_number += 1;
          this.battle_massage[this.massage_number] =
            cha[pasive].name + "に" + this.damage + "のダメージ!";
          this.massage_number += 1;
        }
        if (cha[pasive].hp <= 0) {
          cha[pasive].hp = 0;
          this.battle_massage[this.massage_number] =
            cha[pasive].name + "は死んだ!";
          this.massage_number += 1;
        }
      }
    },
    spell: function (attacker, pasive) {
      cha[pasive].def -= 10;
      if (cha[pasive].def < 0) cha[pasive].def = 0;
      this.battle_massage[this.massage_number] =
        cha[attacker].name + "は「弱化」を唱えた!";
      this.massage_number += 1;
      this.battle_massage[this.massage_number] =
        cha[pasive].name + "の守備力は" + cha[pasive].def + "までさげられた!";
      this.massage_number += 1;
    },
    use_herb: function (user) {
      if (cha[user].hp > 0 && cha[1].hp > 0) {
        if (this.herb > 0) {
          this.damage = Math.floor(9 + Math.random() * 2);
          cha[user].hp += this.damage;
          if (cha[user].hp > cha[user].hp_Maximus)
            cha[user].hp = cha[user].hp_Maximus;
          this.battle_massage[this.massage_number] =
            cha[user].name + "は薬草を使った!";
          this.massage_number += 1;
          if (cha[user].hp == cha[user].hp_Maximus)
            this.battle_massage[this.massage_number] =
              cha[user].name + "のHPは全回復した!";
          else
            this.battle_massage[this.massage_number] =
              cha[user].name + "のHPは" + this.damage + "回復した!";
          this.massage_number += 1;
          this.herb -= 1;
        } else {
          this.battle_massage[this.massage_number] = "薬草が足りない!";
          this.massage_number += 1;
        }
      }
    },
  },
};
</script>
<style>
div.scroll_bar{
  width:500px;
  height:200px;
  overflow:scroll;
  border:1px solid #ccc;
}
</style>