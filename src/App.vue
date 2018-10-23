// 模板 结构
<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/B612Kaji_20180911_101437_479.gif">
    <!-- vue自定义组件 -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <div class="weather-box">
      <!-- 天气预报查询 -->
      <input type="text" v-model="city" @keyup.enter="search">
      <!-- <ul> -->
      <transition-group name="list" tag="ul">
        <li v-for="(item, index) in weatherList" :key="item.date">
          {{item.date}}{{item.high}}~~{{item.low}}---{{item.fengxiang}}
        </li>
      </transition-group>
      <!-- </ul> -->
    </div>
  </div>
</template>

// js代码
<script>
// 导入了 HelloWorld这个单文件组件
// import HelloWorld from './components/HelloWorld.vue'

// 引入axios
import axios from 'axios';

export default {
  // 数据
  data: function() {
    return {
      // 城市
      city: "",
      // 天气信息
      weatherList: []
    };
  },
  methods: {
    search() {
      // 调用接口 获取数据 渲染页面
      // this.$http.get('http://wthrcdn.etouch.cn/weather_mini?city='+this.city)
      // .then(function(response){
      //     // console.log(response);
      //     console.log(this);
      //     // this.weatherList = response.body.data.forecast;
      // })
      // console.log(this);
      // 清空数据
      this.weatherList = [];
      // axios获取数据
      axios
        .get("http://wthrcdn.etouch.cn/weather_mini?city=" + this.city)
        .then(response => {
          // console.log(response);
          // console.log(this);
          this.weatherList = response.data.data.forecast;
        });
    }
  }
};
</script>

// 样式
<style>
img {
  border-radius: 50%;
}

.list-item {
  display: inline-block;
  margin-right: 10px;
}

.list-enter-active,
.list-leave-active {
  transition: all 1s;
}

.list-enter,
        .list-leave-to

        /* .list-leave-active for below version 2.1.8 */
 {
  opacity: 0;
  transform: translateX(100px);
}
body {
  background-color: orange;
}
.music-box,
.weather-box {
  border: 10px solid white;
  background-color: skyblue;
  width: 500px;
}
ul {
}
input {
  height: 40px;
  border-radius: 10px;
  width: 80%;
  margin: 0 auto;
  display: block;
  font-size: 20px;
}
</style>
