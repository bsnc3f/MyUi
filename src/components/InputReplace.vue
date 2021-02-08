<template>
  <div id="app">
    <h2>入力制限を設けたフォーム</h2>
    <p>数字以外の入力をキャンセルするinputフォーム</p>
    <input
      class="inputValue"
      type="text"
      name="inputValue"
      id="inputValue"
      v-model="inputValue"
      @keyup.enter="onKeypressEnter"
      @keypress.46="onKeypressDot"
      @keyup="keyUpHalfSizeRestriction"
    />
    <p>{{ inputValue }}</p>
    <p>setValue= {{ setValue }}</p>
    <p>devidValue= {{ devidValue }}</p>
    <p>sum= {{ sum }}</p>
    <p>min= {{ min }}</p>
    <p>sec= {{ sec }}</p>
    <hr />

    <p>英数字以外の入力をキャンセルするinputフォーム</p>
    <input
      class="inputValue"
      type="text"
      name="inputValue2"
      v-model="inputValue2"
      @keyup.enter="onKeypressEnter"
      @keypress.46="onKeypressDot"
      @keyup="keyUpNumberRestriction"
    />
    <p>{{ inputValue2 }}</p>

    <hr />
    <h2>全角半角への置き換え</h2>
    <div class="form-group">
      <label class="col-md-2 control-label">全角のまま</label>
      <div class="col-md-10">
        <input class="form-control" v-model.trim="a" />
      </div>
    </div>
    <div class="form-group">
      <label class="col-md-2 control-label">全角英数 ⇒ 半角</label>
      <div class="col-md-10">
        <input class="form-control" v-model.trim="b" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      inputValue: "",
      inputValue2: "",
      setValue: "",
      devidValue: "",
      sum: "",
      min: "",
      sec: "",
      a: "",
      b: "",
    };
  },
  methods: {
    sec2min(time) {
      // var hour = Math.floor(time / 60);
      var smin = Math.floor(time / 60);
      var ssec = time % 60;
      this.min = smin;
      this.sec = ssec;
      // this.hour = hour;
    },
    onKeypressEnter: function () {
      this.setValue = this.inputValue;
      // confirm("Enterキーが押されました");
      var endPlus = /[+]$/;
      if (endPlus.test(this.setValue)) {
        alert("該当の文字が含まれています");
      } else {
        this.devidValue = this.setValue.split(/(?=-)+|[+]+/).map(Number);
        // 完成  // this.devidValue = this.setValue.split(/(?=-)+|[+]+/);

        // this.isMinNum(this.devidValue);
        for (let i = 0; i < this.devidValue.length; i++) {
          var tmpArr = this.devidValue[i];
          alert("tmpArr_" + [i] + "=" + tmpArr);

          if (String(tmpArr).length >= 3) {
            this.sec2min(tmpArr);
          }
          var minus = "-";
          this.sum = this.devidValue
            .filter(function (item) {
              return item !== minus;
            })
            .map(Number);

          this.sum = this.sum.reduce((acc, value) => acc + value);
        }

        //1個目の^以降の文字列が欲しければ以下で取得する。
        //https://qiita.com/otami/items/ff8dcaa38a1b16b3cd19
        //  (?<=\^)(.*)

        // アイテムを削除する
        // https://www.it-swarm-ja.tech/ja/javascript/javascript%E3%81%A7%E9%85%8D%E5%88%97%E3%81%8B%E3%82%89%E7%89%B9%E5%AE%9A%E3%81%AE%E8%A6%81%E7%B4%A0%E3%82%92%E5%89%8A%E9%99%A4%E3%81%99%E3%82%8B%E6%96%B9%E6%B3%95/972977169/

        // 配列の中から5未満の数字を除外する
        //https://techacademy.jp/magazine/15575
        // var numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9];
        // function isMinNum(value) {
        //   return (value >= 5);
        // }
        // var filterNum = numbers.filter(isMinNum);
        // confirm(filterNum);
      }
    },
    onKeypressDot: function () {
      confirm("dotキーが押されました");
    },
    keyUpHalfSizeRestriction: function () {
      var tmp_value = this.inputValue;
      if (tmp_value) {
        this.inputValue = tmp_value.replace(/[^0-9+-]/g, "");
        // this.inputValue = tmp_value.replace(/[^0-9+-*]/g, "");
        // this.inputValue = tmp_value.replace(/[^0-9a-zA-Z+-*]/g, "");
      }
    },
    keyUpNumberRestriction: function () {
      var tmp_value2 = this.inputValue2;
      if (tmp_value2) {
        this.inputValue2 = tmp_value2.replace(/[^0-9a-zA-Z]/g, "");
        // this.inputValue2 = tmp_value2.replace(/[^0-9]/g, "");
      }
    },
  },
  watch: {
    a: function (v) {
      this.a = v.replace(/[A-Za-z0-9]/g, function (s) {
        return String.fromCharCode(s.charCodeAt(0) + 65248);
      });
    },
    b: function (v) {
      this.b = v.replace(/[Ａ-Ｚａ-ｚ０-９]/g, function (s) {
        return String.fromCharCode(s.charCodeAt(0) - 65248);
      });
    },
  },
};
</script>


<style scoped>
</style>
