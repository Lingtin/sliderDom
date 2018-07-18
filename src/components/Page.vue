
<template>
  <div class="postbox" :style="computed_style">
    <slot/>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

@Component
export default class Page extends Vue {
    computed_style:object = {width:window.innerWidth+'px'};

    mounted(){
      window.addEventListener('resize',()=>{
          this.computed_style = {width:window.innerWidth+'px'};
      });
    }
}
</script>

<style lang="scss" scoped>
.postbox{
    display: inline-block;
    height: 100%;
    background: green;
    color: #fff;
   .infos h1 {
    margin-bottom: 10px;
    font-size: 50px;
    font-weight: 400;
   }

   .infos h5 {
      background-color: white;
      color: black;
      padding: 4px 12px;
      font-size: 20px;
      font-weight: 300;
      box-shadow: 0px 0px 30px rgba(0, 0, 0, 0.3);
  }
}

</style>
