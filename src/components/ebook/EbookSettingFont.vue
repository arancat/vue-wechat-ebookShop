<template>
  <transition name="slide-up">
    <!-- slide-up滑动也属于transition渐变 -->
    <div class="setting-wrapper" v-show="menuVisible && settingVisible === 0">
      <!-- 一般在条件中，条件最好放在wrapper中settingwrapper  -->
      <!-- v-show="menuVisible && settingVisible === 0"选择的时候如果有多个选项，一定要先做存在性判断 -->
      <div class="setting-font-size">
        <div class="preview" ref="left">
          <!-- ref是vue中的引用信息，http:'https://blog.csdn.net/weixin_41646716/article/details/80455506' -->
          <span :style="styleLeft" ref="leftText">A</span>
        </div>
        <div class="select">
          <div class="select-wrapper" v-for="(item, index) in fontSizeList" :key="index"
               @click="setFontSize(item.fontSize)" ref="item">
                  <!-- 循环v-for  点击事件@click @click=“setFontSize(item.fontSize)”-->
            <div class="line"></div>
            <div class="point-wrapper">
              <div class="point" v-show="defaultFontSize === item.fontSize">
                <div class="small-point"></div>
              </div>
            </div>
            <div class="line"></div>
          </div>
        </div>
        <div class="preview" ref="right">
          <span :style="styleRight" ref="rightText">A</span>
           <!-- <span :style="styleRight" ref="rightText">A</span> -->
        </div>
      </div>
      <div class="setting-font-family" @click.stop="showFontFamilySetting">
        <div class="setting-font-family-text-wrapper">
          <span class="setting-font-family-text">{{defaultFontFamily}}</span>
          <!-- 输出{{xxx}} -->
        </div>
        <div class="setting-font-family-icon-wrapper">
          <span class="icon-forward"></span>
          <!-- 一般icon图标等用span显示 -->
        </div>
      </div>
    </div>
  </transition>
  <!-- transition可以放在大的框架，其中的元素可以包含多个transition -->
</template>

<script type="text/ecmascript-6">
// <script type="text/ecmascript-6" >
  import { ebookMixin } from '@/utils/mixin'
import { threadId } from 'worker_threads';
//引入 { ebookMinxin }
  export default {
    mixins: [ebookMixin],
    //data(){}
    data() {
      return {
        styleLeft: {},
        styleRight: {}
      }
    },
    //watch: {}
    watch: {
      settingVisible(v) {
        if (v === 0) {
          this.$nextTick(() => {
            this.genStyle()
          })
        }
      }
    },
    //methods:{}
    methods: {
      genStyle() {
      //   genStyle根样式方法-》
      //   const left = this.$refs.left.getBoundingClientRect().width
      //   获取某个元素相对于视窗的位置集合。集合中有top, right, bottom, left等属性。
      // const right = this.$refs.left.getBoundingClientRect().width
      // const leftText = this.$refs.leftText.getBoundingClientRect().width
      // const rightText = this.$refs.rightText.getBoundingClientRect().width
      // const item = this.$refs.item[0].getBoundingClientRect().width
      // this.styleLeft = {
      //   marginLeft: (left + item -leftText ) / 2 + 'px',
      //   fontSize: this.fontSizeList[0].fontSize + 'px'
      // }
      // this.styleRight = {
      //   marginRight: (right + item - rightText ) / 2 + 'px',
      //   fontSize: this.fontSizeList[this.fontSizeList.length - 1].fontSize + 'px'
      // }
        const left = this.$refs.left.getBoundingClientRect().width
        const right = this.$refs.left.getBoundingClientRect().width
        const leftText = this.$refs.leftText.getBoundingClientRect().width
        const rightText = this.$refs.leftText.getBoundingClientRect().width
        const item = this.$refs.item[0].getBoundingClientRect().width
        this.styleLeft = {
          marginLeft: (left + item - leftText) / 2 + 'px',
          fontSize: this.fontSizeList[0].fontSize + 'px'
        }
        this.styleRight = {
          marginRight: (right + item - rightText) / 2 + 'px',
          fontSize: this.fontSizeList[this.fontSizeList.length - 1].fontSize + 'px'
        }
      }
    }
  }
</script>

<style lang="scss" rel="stylesheet/scss" scoped>
  @import "../../assets/styles/global";

  .setting-wrapper {
    position: absolute;
    bottom: px2rem(48);
    left: 0;
    z-index: 190;
    display: flex;
    flex-direction: column;
    width: 100%;
    height: px2rem(90);
    box-shadow: 0 px2rem(-8) px2rem(8) rgba(0, 0, 0, .15);
    .setting-font-size {
      flex: 2;
      display: flex;
      height: 100%;
      .preview {
        flex: 0 0 px2rem(40);
        @include center;
      }
      .select {
        display: flex;
        flex: 1;
        .select-wrapper {
          flex: 1;
          display: flex;
          align-items: center;
          &:first-child {
            .line {
              &:first-child {
                border-top: none;
              }
            }
          }
          &:last-child {
            .line {
              &:last-child {
                border-top: none;
              }
            }
          }
          .line {
            flex: 1;
            height: 0;
          }
          .point-wrapper {
            position: relative;
            flex: 0 0 0;
            width: 0;
            height: px2rem(7);
            .point {
              position: absolute;
              top: px2rem(-8);
              left: px2rem(-10);
              width: px2rem(20);
              height: px2rem(20);
              border-radius: 50%;
              box-shadow: 0 px2rem(4) px2rem(4) rgba(0, 0, 0, .15);
              @include center;
              .small-point {
                width: px2rem(5);
                height: px2rem(5);
                border-radius: 50%;
              }
            }
          }
        }
      }
    }
    .setting-font-family {
      flex: 1;
      font-size: px2rem(14);
      @include center;
      .setting-font-family-text-wrapper {
        @include center;
      }
      .setting-font-family-icon-wrapper {
        @include center;
      }
    }
  }
</style>
