<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
  export default {}
  document.addEventListener('DOMContentLoaded', () => {
    let fontSize = window.innerWidth / 10
    fontSize = fontSize > 50 ? 50 : fontSize
    const html = document.querySelector('html')
    html.style.fontSize = fontSize + 'px'
  })
  export default {}
  document.addEventListener('DOMContentLoaded', () => {
    //document.addEventListener DOM内容加载完成之后—— ？ 还有其他的什么状态？
    let fontSize = window.innerWidth / 10
    //此处let  es6 如果用var 的区别呢？哪个环境的适应性更好？
    fontSize = fontSize > 50 ? 50 : fontSize
    //三目运算符 —— 注意格式（空格）
    const html = document.querySelector('html')
    //const 与 let  var的适用场景 http:"https://blog.csdn.net/qq_36784628/article/details/80966826"
    //html意义是什么？
    // querySelector——id=dome仅一个 + class... http://" https://www.runoob.com/jsref/met-document-queryselector.html "
  })
</script>

<style scoped>
  #app {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    z-index: 0;
    width: 100%;
    height: 100%;
    background: #7d8188;
    overflow: hidden;
  }
</style>
