<template>
  <div :id="vivusId">
  </div>
</template>

<script>
import Vivus from 'vivus'
export default {
  name: 'app',
  data () {
    return {
      svg: null
    }
  },
  props:{
    vivusId:{
      type:String,
      default:'vivusId'
    },
    file:{
      type:String,
      default: '' // 文件路径 绝对路径
    },
    type:{
      type:String,
      default:'delayed' // 动画类型
    },
    duration:{
      type:Number ,
      default:200  // 过渡时间
    },
    start:{
      type:String,
      default:'inViewport' // 定义如何开始
    },
    onReady:{
      type:Function,
      default:function(){
      }
    },
    callBack:{
      type:Function,
      default:function(){
      }
    },
    pathTiming:{
      type:String,
      default:'EASE'
    },
    animTiming:{
      type:String,
      default:'EASE'
    },
    dashGap:{
      type:Number,
      default:2
    },
    forceRender:{
      type:Boolean,
      default:true
    },
    reverseStack:{
      type:Boolean,
      default:false
    }
  },
  mounted:function(){
    this.initVueSvg()
  },
  methods:{
    initVueSvg(obj) {
      let pathTimingFunction,animTimingFunction
      switch (this.pathTiming) {
        case 'EASE':
          pathTimingFunction = Vivus.EASE
          break;
        case 'EASE_IN':
          pathTimingFunction = Vivus.EASE_IN
        break;
        case 'EASE_OUT':
          pathTimingFunction = Vivus.EASE_OUT
        break;
        case 'EASE_OUT_BOUNCE':
          pathTimingFunction = Vivus.EASE_OUT_BOUNCE
        break;
        default:
          break;
      }
       switch (this.animTiming) {
        case 'EASE':
          animTimingFunction = Vivus.EASE
          break;
        case 'EASE_IN':
          animTimingFunction = Vivus.EASE_IN
        break;
        case 'EASE_OUT':
          animTimingFunction = Vivus.EASE_OUT
        break;
        case 'EASE_OUT_BOUNCE':
          animTimingFunction = Vivus.EASE_OUT_BOUNCE
        break;
        default:
          break;
      }
      this.svg = new Vivus(this.vivusId,
      {
      type: this.type,
      duration: this.duration,
      animTimingFunction: Vivus.EASE,
      file:this.file,
      onReady:this.onReady,
      pathTimingFunction:pathTimingFunction,
      animTimingFunction:animTimingFunction,
      dashGap:this.dashGap,
      forceRender:this.forceRender,
      reverseStack:this.reverseStack
      },this.callBack)
    },
    stop(){
      this.svg.stop()
    }, // 停止
    reset(){
      this.svg.reset()
    }, // 重绘
    play(speed,fun){
      this.svg.play(speed,fun) 
    },// 播放
    finish(){
      this.svg.finish()
    }, // 完成
    setFrameProgress(progress){
      this.svg.setFrameProgress(progress) // 0~1
    }, //设置进度
    getStatus(){
      this.svg.getStatus()
    }, // 获取状态
    destroy(){
      this.svg.destroy()
    }
  },
  destroyed(){
    this.svg.destroy()
  }
}
</script>

<style>

</style>
