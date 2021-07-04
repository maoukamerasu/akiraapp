<template>
  <div id="Convenient">
    <table id="table">
      <tr>
        <td colspan="3">
          <input type="munber" id="number" v-model="textbox" maxlength="0" />
        </td>
      </tr>
      <tr v-for="i in 3" v-bind:key="i.id">
        <th v-for="l in 3" v-bind:key="l.id">
          <button @click="input(number[i - 1][l - 1])">
            {{ number[i - 1][l - 1] }}
          </button>
        </th>
      </tr>
      <tr>
        <th>
          <button @click="input(0)">0</button>
        </th>
        <th>
          <button @click="plus">+</button>
        </th>
        <th>
          <button @click="minus">-</button>
        </th>
      </tr>
      <tr>
        <th>
          <button @click="times">×</button>
        </th>
        <th>
          <button @click="divided_by">÷</button>
        </th>
        <th>
          <button @click="equal">=</button>
        </th>
      </tr>
    </table>
  </div>
</template>
<script>
export default {
  el: "Convenient",
  data() {
    return {
      number: [
        [1, 2, 3],
        [4, 5, 6],
        [7, 8, 9],
      ],
      value: [0, 0],
      textbox: 0,
      Calculation: 0,
      Maximus: 99999999,
    };
  },
  methods: {
    input: function (i) {
      if (this.Calculatio == 5) {
        this.textbox = 0;
        this.Calculatio = 0;
      }
      if (this.textbox * 10 + i < this.Maximus)
        this.textbox = this.textbox * 10 + i;
    },
    plus: function () {
      this.value[0] = this.textbox;
      if (this.Calculation != 0) this.value[1] = 0;
      (this.Calculation = 1), (this.textbox = 0);
    },
    minus: function () {
      this.value[0] = this.textbox;
      if (this.Calculation != 0) this.value[1] = 0;
      (this.Calculation = 2), (this.textbox = 0);
    },
    times: function () {
      this.value[0] = this.textbox;
      if (this.Calculation != 0) this.value[1] = 0;
      (this.Calculation = 3), (this.textbox = 0);
    },
    divided_by: function () {
      this.value[0] = this.textbox;
      if (this.Calculation != 0) this.value[1] = 0;
      (this.Calculation = 4), (this.textbox = 0);
    },
    equal: function () {
      if (this.value[1] == 0) this.value[1] = this.textbox;
      switch (this.Calculation) {
        case 1:
          this.textbox = this.value[0] + this.value[1];
          break;
        case 2:
          this.textbox = this.value[0] - this.value[1];
          break;
        case 3:
          this.textbox = this.value[0] * this.value[1];
          break;
        case 4:
          this.textbox = this.value[0] / this.value[1];
          if (this.value[0] == this.value[1]) this.textbox = this.Maximus;
          break;
      }
      this.value[0] = this.textbox;
      if (this.textbox > this.Maximus) this.textbox = this.Maximus;
      this.Calculatio = 5;
    },
  },
};
</script>
<style>
#table {
  background-color: #000000;
  border: 15px solid #525;
}
#number {
  height: 32px;
  width: 145px;
  font-size: 30px;
  background-color: #888888;
}
#table button {
  background-color: #663520;
  height: 38px;
  width: 50px;
  font-size: 29px;
}
</style>