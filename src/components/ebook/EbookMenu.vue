<template>
<!--HTML内容模板(template)元素是一种用于保存客户端内容机制,该内容在加载页面时不会呈现,
但随后可以在运行时使用JavaScript实例化。-->
  <div class="ebook-menu">
    <!--菜单，上划（transition  过渡css，适用于有动态变化的界面：滚动，增删？-->
    <transition name="slide-up">
      <!--注意div套div修改   ：class简写-->
      <!--查看vue自写简写脚本——>收藏夹-->
      <div class="menu-wrapper" :class="{'hide-box-shadow': settingVisible >= 0 || !menuVisible}"
           v-show="menuVisible">
      <div class="menu-wrapper" :class="{'hide-box-shadow': settingVisible >= 0 || !menuVisible }">
<!--menuwrapper出现的原因是  setting》=0或者菜单不存在-->
      </div>
        <div class="icon-wrapper" :class="{'selected': settingVisible === 3}">
        <div>
          <!-- //selected选择-（同一系列的选择selected 当参数===3——》为何使用绝对等于？） -->
        </div>
          <span class="icon-menu" @click="showSetting(3)"></span>
          <!-- <span class="icon-menu" @click="showSetting(3)"> @click点击事件缩写</span> -->
          <!-- 图片的显示点击事件——重点在图片，选用的包裹是span -->
        </div>
        <div class="icon-wrapper" :class="{'selected': settingVisible === 2}">
          <span class="icon-progress" @click="showSetting(2)"></span>
        </div>
        <div class="icon-wrapper" :class="{'selected': settingVisible === 1}">
          <span class="icon-bright" @click="showSetting(1)"></span>
        </div>
        <div class="icon-wrapper" :class="{'selected': settingVisible === 0}">
          <span class="icon-A" @click="showSetting(0)"></span>
          <!-- 选择项最好是从0开始为事件项 -->
        </div>
      </div>
    </transition>
    <!-- 以下是自定义的组件：组件用xx-cc-vv组成 -->
    <ebook-setting-font></ebook-setting-font>
    <ebook-setting-font-popup></ebook-setting-font-popup>
    <ebook-setting-theme></ebook-setting-theme>
    <ebook-setting-progress></ebook-setting-progress>
    <ebook-slide></ebook-slide>
    <ebook-speaking-icon></ebook-speaking-icon>
  </div>
</template>

<script type="text/ecmascript-6">
//script中 用来让编辑器识别vue文件中的es6语法 ecmascript-6
  import EbookSettingFont from './EbookSettingFont'
  import EbookSettingFont from './EbookSettingFont'
  // 引入 EbookSettingFont组件从此文件的./EbookSettingFontvue文件 需要使用此组件就需要引入
  import EbookSettingFontPopup from './EbookSettingFontPopup'
  import EbookSettingTheme from './EbookSettingTheme'
  import EbookSettingProgress from './EbookSettingProgress'
  import EbookSpeakingIcon from './EbookSpeakingIcon'

  import EbookSlide from './EbookSlide'
  // import { ebookMixin } from '@/utils/mixin'
  // 引入ebookmixin混入？
  import { ebookMixin } from '@/utils/mixin'

  export default {
    // script js 中的export defaulet
    // 添加混入的数据 and组件（什么组件呢？）
    // mixins :[ebookMixin],
    // components: {
    //   EbookSettingFont,
    //   EbookSettingFontPopup,
    //   EbookSpeakingIcon,
    //   EbookSettingTheme,
    //   EbookSettingProgress,
    //   EbookSettingFontPopup
    // }
    mixins: [ebookMixin],
    components: {
      EbookSettingFontPopup,
      EbookSlide,
      EbookSettingProgress,
      EbookSettingFont,
      EbookSettingTheme,
      EbookSpeakingIcon
    }
  }
</script>

<style lang="scss" rel="stylesheet/scss" scoped>
// style--css ,lang语言scss lang="scss" rel="stylesheet/scss" 
//scoped--以表示它的样式作用于当下的模块，很好的实现了样式私有化的目的
  @import "../../assets/styles/global";
  //引style的global  scss


// .menu-wrapper {
//   position:absolute;
//   bottom: 0;
//   left:0;
//   z-index:200;
//   display:flex;//流式布局
//   width: 100%;
//   height: px2rem(48);
//   box-shadow: 0 px2rem(-8) px2rem(8) rgba(0, 0, 0, .15);
//   font-size: px2rem(22);
//   &.hide-box-shadow {
//     box-shadow: none;
//   }
  // 在scss中做逻辑处理，选中& ——class
  //您可以使用＆字符选择父级选择器。 它告诉父选择器应该插入的位置。
  //http:'https://lixh1986.iteye.com/blog/2428306'

  .menu-wrapper {
    position: absolute;
    bottom: 0;
    left: 0;
    z-index: 200;
    display: flex;
    width: 100%;
    height: px2rem(48);
    box-shadow: 0 px2rem(-8) px2rem(8) rgba(0, 0, 0, .15);
    font-size: px2rem(22);
    &.hide-box-shadow {
      box-shadow: none;
    }
    .icon-wrapper {
      flex: 1;
      // @include center;
      // 添加center的scss包
      @include center;
      .icon-progress {
        font-size: px2rem(24);
      }
      .icon-A {
        font-size: px2rem(20);
      }
    }
  }
</style>
