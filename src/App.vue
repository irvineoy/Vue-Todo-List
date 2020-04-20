<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <div class="splash-container">
      <div class="splash">
      <h1 class="splash-head">Vue TODO List</h1>
      </div>
    </div>
    <form class="pure-form">
      <fieldset>
          <legend>共有 {{todoArray.length}} 个计划，已完成 {{computed}} 个，未完成 {{todoArray.length-computed}} 个。</legend>
          <input class="pure-u-18-24" type="text" placeholder="请输入您的任务" v-model="input">
          <div class="pure-u-2-24"></div>

          <button type="submit" @click.prevent="add()" class="pure-button pure-button-primary pure-u-4-24">添加任务</button>
      </fieldset>
    </form>
    <!-- <div class="pure-menu pure-menu-horizontal">
      <ul class="pure-menu-list pure-u-1-1">
          <li class="pure-menu-item pure-menu-selected pure-u-1-3"><a href="#" class="pure-menu-link">所有计划</a></li>
          <li class="pure-menu-item pure-u-1-3"><a href="#" class="pure-menu-link">已完成</a></li>
          <li class="pure-menu-item pure-u-1-3"><a href="#" class="pure-menu-link">未完成</a></li>
      </ul>
    </div> -->
    <button class="pure-button pure-u-1-3" :class="cur==1?'pure-button-primary':''" @click="filterItem(1)">所有计划</button>
    <button class="pure-button pure-u-1-3" :class="cur==2?'pure-button-primary':''" @click="filterItem(2)">已完成</button>
    <button class="pure-button pure-u-1-3" :class="cur==3?'pure-button-primary':''" @click="filterItem(3)">未完成</button>
    <div class="pure-menu">
      <!-- <span class="pure-menu-heading">Yahoo Sites</span> -->
      <!-- <ul class="pure-menu-list" style="padding:0,0,0,0;"> -->

      <ul class="pure-menu-list pure-u-1-1">
        <li v-for="(v,i) in newArray" :key="i" class="pure-menu-item pure-u-1-1" style="margin-top:1em">
            <div class="pure-u-2-24"><input type="checkbox" v-model="v.check"/></div>
            <div class=" pure-u-18-24" :style="v.check?'text-decoration:line-through':''">{{v.content}}</div>
            <button class="pure-button pure-u-4-24" @click="del(v)">删除</button>
        </li>
      </ul>
    </div>
    
  </div>
</template>




// js
<script>
// import HelloWorld from './components/HelloWorld.vue'
export default {
  name: 'App',
  components: {
    // HelloWorld
  },
  data(){
    return{
      newArray:[],
      todoArray:[
        {check: false, content:"待完成任务1"}, // check == false: means have not been done
        {check: false, content:"待完成任务2"}
      ],
      cur:1
    }
  },
  methods:{
    add(){
      if(!this.input) return;
      this.todoArray.unshift({check:false, content:this.input});
      this.input = "";
    },
    del(v){
      var i = this.todoArray.findIndex(item=>item.content == v.content);
      this.todoArray.splice(i, 1);
      this.filterItem(this.cur);
    },
    filterItem(i){
      this.cur = i
      switch(i){
        case 2:
          this.newArray = this.todoArray.filter(item=>item.check);
          break;
        case 3:
          this.newArray = this.todoArray.filter(item=>!item.check);
          break;
        default:
          this.newArray = this.todoArray;
      }
    }
  },
  mounted(){
    this.filterItem(this.cur);
  },
  computed:{
    computed(){
      return this.todoArray.filter(item=>item.check).length;
    }

  }
}
</script>


// CSS
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.custom-restricted-width {
    /* To limit the menu width to the content of the menu: */
    /* display: inline-block; */
    /* Or set the width explicitly: */
    /* width: 50em; */
    Width: 50%；
}
</style>
