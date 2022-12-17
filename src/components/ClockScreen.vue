<template>
  <div class="container">
    <div class="clock" >
      <div class="date">
        <p>{{ year }}/{{ month }}/{{ day }}</p>
      </div>
      <div class="time">
        <p>
          {{ hours }}:{{ minutes }}<span class="seconds">:{{ seconds }}</span>
        </p>
      </div>
    </div>
    <div class="button" v-on:click="showMessage()">
      <p>
        10秒後にアラームを設定
      </p>
    </div>
  </div>

</template>

<script>

/*****

処理の流れ
1. mountedに定義されたコードが実行される。
2. setInterval()で１秒ごとに現在の時間を表示されるようになる。
3. 画面が何度も表示されるたび、computedでデータが加工される。
4. templateの各用をが表示される。

*****/

export default{
  name: "ClockScreen",
  data(){
    return{
      date: new Date(),
    };
  },
  // computedとは
  // dataで取得した情報を加工する
  computed: {
    year(){
      return this.date.getFullYear();
    },
    month(){
      return this.date.getMonth() + 1;
    },
    day(){
      return this.dateTimePadding(this.date.getDate());
    },
    hours(){
      return this.dateTimePadding(this.date.getHours());
    },
    minutes(){
      return this.dateTimePadding(this.date.getMinutes());
    },
    seconds(){
      return this.dateTimePadding(this.date.getSeconds());
    }
  },
  // mountedとは
  // 画面のHTMLが用意された時点で読み込まれる。
  // 画面が表示されるときに一番最初に読み込まれる。
  // プログラムが画面に読み込まれるまでの処理を「ライフサイクル」という。 
  mounted(){
    this.setDate();
    setInterval(() => this.setDate(), 1000)
  },
  // methodsとは
  // メソッド（処理）を記述する領域
  methods: {
    dateTimePadding(num){
      return("0" + num).slice(-2);
    },
    setDate(){
      this.date = new Date();
    },
    showMessage(){
      window.setTimeout(() => {
        alert("10秒経過しました")
      }, 10000);
    }
  }
}
</script>

<style scoped>
.container{
  height: 100%;
  display: flex;
  flex-flow: column;
  justify-content: center;
  align-items: center;
  background-color: #262626;
}
p{
  margin: 0px;
}
.date,
.time{
  font-weight: 700;
  color: #00ff01;
}
.date{
  font-size: 32px;
  text-align: right;
}
.time{
  font-size: 140px;
}
.seconds{
  font-size: 60px;
}
.button{
  border: 1px solid #fcfcfc;
  text-align: center;
  padding: 15px 10px;
  color:#fcfcfc;
  cursor: pointer;
}
</style>