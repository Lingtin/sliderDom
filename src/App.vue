<template>
  <div id="app">
    <Slider v-model="currentIndex">
        <Page v-for="(item,index) in List" :key="index">{{item}}</Page>
    </Slider>

    <button class='button' @click="delList">删除</button>
    <button class='button' @click="addList">添加</button>
  </div>
</template>

<script lang="ts">
import { Component,Provide, Vue } from 'vue-property-decorator';
import Slider from './components/Slider.vue';
import Page from './components/Page.vue';

@Component({
  components: {
    Slider,Page
  },
})
export default class App extends Vue {
  currentIndex:number=0;

  List:Array<number> = [1,2,3];

  addList(){
    this.List.push(this.List.length+1)
  }

  delList(){
    this.List.splice(this.currentIndex,1);
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
html,body{
  height: 100%;
  width: 100%;
  padding: 0;
  margin: 0;
}
.button{
  margin: 40px 40px;
  width: 120px;
  height: 38px;
  background: goldenrod;
  border: none;
  color: #fff;
  outline: none;
  cursor: pointer;
  &:hover{
    background:green;
  }
}
</style>
