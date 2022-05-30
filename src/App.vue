<template>
  <div class="header">
    <ul class="header-button-left">
      <li>Cancel</li>
    </ul>
    <ul class="header-button-right">
      <li @click="step++;">Next</li>
    </ul>
    <img src="./assets/logo.png" class="logo" />
  </div>
 
  <ContainerView :instardata="instardata2" :step="step" :imageUrl="imageUrl" />

  <button @click="getPostData">더보기</button>

  <div class="footer">
    <ul class="footer-button-plus"> 
      <input type="file" id="file" class="inputfile" @change="fnImageUpload"/>
      <label for="file" class="input-plus">+</label>
    </ul>
 </div>

  <!-- <div v-if="tabState == 0">내용0</div>
  <div v-if="tabState == 1">내용1</div>
  <div v-if="tabState == 2">내용2</div>
  <button @click="tabState = 0">버튼0</button>
  <button @click="tabState = 1">버튼1</button>
  <button @click="tabState = 2">버튼2</button>
  <div style="margin-top : 20px;"></div> -->

</template>

<script>

import ContainerView from './components/ContainerView.vue'

import instardata from './assets/instardata.js'

import axios from 'axios';

export default {
  name: 'App',
  components: {
    ContainerView
  },
  data() {
    return {
      instardata2 : instardata,
      clickcount : 0,
      tabState : 0,
      step : 0,
      imageUrl : '',
    }
  },
  methods : {
    getPostData() {
      axios.get('https://codingapple1.github.io/vue/more'+this.clickcount+'.json'
      ).then(res =>{
        //console.log(res);  
        console.log(this.instardata2);  
        this.instardata2.push(res.data);
        this.clickcount = this.clickcount+1;
      }).catch( err =>{
        console.log(err);
      })

    },
    fnImageUpload(e){
      console.log('------- 파일업로드');
      console.log(e.target.files);
      var files = e.target.files;
      this.imageUrl = URL.createObjectURL(files[0]);
      console.log(this.imageUrl);
      this.step = 1;

    }
  },
}
</script>

<style>
body {
  margin: 0;
}
ul {
  padding: 5px;
  list-style-type: none;
}
.logo {
  width: 22px;
  margin: auto;
  display: block;
  position: absolute;
  left: 0;
  right: 0;
  top: 13px;
}
.header {
  width: 100%;
  height: 40px;
  background-color: white;
  padding-bottom: 8px;
  position: sticky;
  top: 0;
}
.header-button-left {
  color: skyblue;
  float: left;
  width: 50px;
  padding-left: 20px;
  cursor: pointer;
  margin-top: 10px;
}
.header-button-right {
  color: skyblue;
  float: right;
  width: 50px;
  cursor: pointer;
  margin-top: 10px;
}
.footer {
  width: 100%;
  position: sticky;
  bottom: 0;
  padding-bottom: 10px;
  background-color: white;
}
.footer-button-plus {
  width: 80px;
  margin: auto;
  text-align: center;
  cursor: pointer;
  font-size: 24px;
  padding-top: 12px;
}
.sample-box {
  width: 100%;
  height: 600px;
  background-color: bisque;
}
.inputfile {
  display: none;
}
.input-plus {
  cursor: pointer;
}
#app {
  box-sizing: border-box;
  font-family: "consolas";
  margin-top: 60px;
  width: 100%;
  max-width: 460px;
  margin: auto;
  position: relative;
  border-right: 1px solid #eee;
  border-left: 1px solid #eee;
}
</style>
