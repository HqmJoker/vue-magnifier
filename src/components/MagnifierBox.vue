<template>
  <div class="magnifier" ref="magnifier" @mouseover="showZoomBox" @mouseout="hiddenZoomBox" @mousemove="moveCursor">
    <img class="magnifier-thumbnail" :src="imgUrl" alt="缩略图" />
    <span class="magnifier-cursor" :style="cursorStyle"></span>
    <div class="magnifier-area" v-show="isShowCursor">
      <img :src="imgUrl" alt="放大图" :style="magnifierAreaStyle" />
    </div>
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
      },
      magnifierAreaStyle() {
        return {
          // width: this.cursorWidth + 'px',
          // height: this.cursorHeight + 'px',
          left: -this.cursorLeft * 3 + 'px', // 此处相对位置需要取负值，因为光标往下移动时，图片需要相对往上移才能显示对应的区域
          top: -this.cursorTop * 3 + 'px'
        }
      }
    } ,
    methods: {
      showZoomBox(event) {
        const halfCursor = this.cursorWidth / 2;
        const left = event.clientX - this.magnifierBoxLeft - halfCursor;
        const top = event.clientY - this.magnifierBoxTop - halfCursor;
        // 处理光标左侧
        if(left < 0) { // 防止左侧溢出
          this.cursorLeft = 0;
        }
        if(left >= 0 && left <= 200 - this.cursorWidth) {
          this.cursorLeft = left;
        }
        if(left > 200 - this.cursorWidth) { // 防止右侧溢出
          this.cursorLeft = 200 - this.cursorWidth;
        }
        // 处理光标顶部
        if(top < 0) { // 防止顶部溢出
          this.cursorTop = 0;
        }
        if(top >= 0 && top <= 200 - this.cursorWidth) {
          this.cursorTop = top;
        }
        if(top > 200 - this.cursorWidth) { // 防止底部溢出
          this.cursorTop = 200 - this.cursorWidth;
        }
        this.isShowCursor = true;
      },
      hiddenZoomBox() {
        this.isShowCursor = false;
        this.cursorLeft = 0;
        this.cursorTop = 0;
      },
      moveCursor(event) {
        const halfCursor = this.cursorWidth / 2;
        const left = event.clientX - this.magnifierBoxLeft - halfCursor;
        const top = event.clientY - this.magnifierBoxTop - halfCursor;
        // 处理光标左侧
        if(left < 0) { // 防止左侧溢出
          this.cursorLeft = 0;
        }
        if(left >= 0 && left <= 200 - this.cursorWidth) {
          this.cursorLeft = left;
        }
        if(left > 200 - this.cursorWidth) { // 防止右侧溢出
          this.cursorLeft = 200 - this.cursorWidth;
        }
        // 处理光标顶部
        if(top < 0) { // 防止顶部溢出
          this.cursorTop = 0;
        }
        if(top >= 0 && top <= 200 - this.cursorWidth) {
          this.cursorTop = top;
        }
        if(top > 200 - this.cursorWidth) { // 防止底部溢出
          this.cursorTop = 200 - this.cursorWidth;
        }
        this.isShowCursor = true;
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
  .magnifier-area {
    width: 200px;
    height: 200px;
    position: absolute;
    top: 0;
    right: 0;
    transform: translateX(100%);
    background-color: #e8e8e8;
    overflow: hidden;
  }
  .magnifier-area img {
    width: 600px;
    position: absolute;
  }
</style>
