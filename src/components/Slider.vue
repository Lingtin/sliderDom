
<template>
    <div id="slider">
        <div class="postarea">
            <div :style="computed_left" class="posts">
                <slot></slot>
            </div>
        </div>
        <div @click="delta(-1)" class="control_left icon iconfont icon-jiantou-zuo"></div>
        <div @click="delta(1)" class="control_right icon iconfont icon-jiantou-you"></div>
    </div>
</template>

<script lang="ts">
import { Component,Prop,Model,Watch,Inject, Vue } from 'vue-property-decorator';

@Component
export default class Slider extends Vue{
    @Prop({default:0,type:Number})
    @Model('change') currentIndex!:number;

    @Watch('now_index')
    onCurrentIndex(val:number,oldval:number){
        this.$emit('change', val)
    }

    computed_left:object = {left:'0px'};
    now_index:number = this.currentIndex;
    workslength:number= 0;
    span:number = window.innerWidth;

    delta(d:number){
        
        this.now_index = (this.now_index+d+this.workslength)%(this.workslength);
        this.computed_left = this.sumLeft();

        let lengt = document.querySelectorAll('.posts>div').length;
        this.workslength = lengt;
    }

    sumLeft(){
        let w = window.innerWidth;
        let result={left:(-this.now_index*w)+'px'};
        return result;
    }

    bg_css(url:string){
        return "background-image:url("+url+")";
    }

    onSize(){
        this.computed_left = this.sumLeft();
    }

    mounted(){
        this.onSize();
        window.addEventListener('resize',()=>{
            this.onSize();
        });
        let lengt = document.querySelectorAll('.posts>div').length;
        this.workslength = lengt;
    }
}
</script>

<style lang="scss" scoped>
// 导入 阿里巴巴 font 的图标库
@import url('//at.alicdn.com/t/font_750992_y5my5zpt7ef.css');

.postarea {
    height: 300px;
    white-space: nowrap;
}

.posts {
    height: 100%;
    position: relative;
    transition: 0.5s;
}

#slider {
    width: 100%;
    height: 100%;
    display: flex;
    align-items: center;
    overflow: hidden;
}

.control_left, .control_right {
    width: 40px;
    height: 40px;
    position: fixed;
    color: white;
    font-size: 38px;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
    opacity: 0.5;
    &:hover{
        opacity: 1;
        transition: 0.5s 0s;
    }
}

.control_left {
    left: 50px;
}

.control_right {
    right: 50px;
}


</style>
