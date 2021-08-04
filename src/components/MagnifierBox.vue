<template>
  <div class="magnifier" ref="magnifier" @mouseover="showZoomBox" @mouseout="hiddenZoomBox" @mousemove="moveCursor">
    <img class="magnifier-thumbnail" :src="imgUrl" alt="缩略图"  />
    <span v-show="isShowCursor" class="magnifier-cursor" :style="cursorStyle" ></span>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        cursorWidth: 50, // 光标宽度 
        cursorHeight: 50, // 光标高度 
        cursorLeft: 0, // 光标圈相对放大区域左侧距离
        cursorTop: 0, // 光标圈相对放大区域顶部距离
        isShowCursor: false, // 是否显现光圈
        magnifierBoxLeft: 0, // 图片原始区域位置，用于移入时计算放大区域位置
        magnifierBoxTop: 0, // 图片原始区域位置，用于移入时计算放大区域位置
      } 
    },
    props: {
      imgUrl: {
        type: String,
        required: true,
      }
    },
    mounted() {
      this.magnifierBoxLeft = this.$refs.magnifier.offsetLeft;
      this.magnifierBoxTop = this.$refs.magnifier.offsetTop;
    },
    computed: {
      cursorStyle() {
        return {
          width: this.cursorWidth + 'px',
          height: this.cursorHeight + 'px',
          left: this.cursorLeft + 'px',
          top: this.cursorTop + 'px'
        }
      }
    } ,
    methods: {
      showZoomBox(event) {
        console.log(event)
        const halfCursor = this.cursorWidth / 2;
        const left = event.clientX - this.magnifierBoxLeft - halfCursor; // 863 860 25
        const top = event.clientY - this.magnifierBoxTop - halfCursor;
        // 处理光标左侧
        if(left < halfCursor) { // 防止左侧溢出
          this.cursorLeft = 0;
        }
        if(left >= halfCursor && left <= 200 - halfCursor) {
          this.cursorLeft = left
        }
        if(left > 200 - halfCursor) { // 防止右侧溢出
          this.cursorLeft = 200 - halfCursor;
        }
        // 处理光标顶部
        if(top < halfCursor) { // 防止顶部溢出
          this.cursorTop = 0;
        }
        if(top >= halfCursor && top <= 200 - halfCursor) {
          this.cursorTop = top
        }
        if(top > 200 - halfCursor) { // 防止底部溢出
          this.cursorTop = 200 - halfCursor;
        }
        this.isShowCursor = true;
      },
      hiddenZoomBox() {
        console.log(222)
        this.isShowCursor = false;
        this.cursorLeft = 0;
        this.cursorTop = 0;
      },
      moveCursor(event) {
        // console.log(event)
        // const halfCursor = this.cursorWidth / 2;
        // const left = event.offsetX - halfCursor;
        // const top = event.offsetY - halfCursor;
        // // 处理光标左侧
        // if(left < halfCursor) { // 防止左侧溢出
        //   this.cursorLeft = 0;
        // }
        // if(left >= halfCursor && left <= 200 - halfCursor) {
        //   this.cursorLeft = left
        // }
        // if(left > 200 - halfCursor) { // 防止右侧溢出
        //   this.cursorLeft = 200 - halfCursor;
        // }
        // // 处理光标顶部
        // if(top < halfCursor) { // 防止顶部溢出
        //   this.cursorTop = 0;
        // }
        // if(top >= halfCursor && top <= 200 - halfCursor) {
        //   this.cursorTop = top
        // }
        // if(top > 200 - halfCursor) { // 防止底部溢出
        //   this.cursorTop = 200 - halfCursor;
        // }
        // this.isShowCursor = true;
      },
    }
  }
</script>

<style scoped>
  .magnifier {
    position: relative;
    width: 200px;
    height: 200px;
    margin: 0 auto;
    background-color: pink;
  }
  .magnifier-thumbnail {
  }
  .magnifier-cursor {
    position: absolute;
    top: 0;
    left: 0;
    z-index: 1;
    display: inline-block;
    background-color: rgba(255, 255, 255, .5);
    width: 50px;
    height: 50px;
    cursor: crosshair;
  }
</style>
