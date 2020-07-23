<template>
  <div class="hello" id="container">

  </div>
</template>

<script>
import AMap from 'AMap';
export default {
  name: 'HelloWorld',
  created() {

        },
  mounted(){
      this.loadmap()
  },
  methods: {
      loadmap(){
          let map = new AMap.Map('container', {
              center: [116.397428, 39.90923],
              resizeEnable: true,
              zoom: 10,
              //lang: 'en'
          });
          let infoWindow = new AMap.InfoWindow({ //创建信息窗体
            isCustom: false,  //使用自定义窗体
            content:'<div>信息窗体</div>', //信息窗体的内容可以是任意html片段
            offset: new AMap.Pixel(16, -45)
          });
          let onMarkerClick  =  function(e) {
              infoWindow.open(map, e.target.getPosition());//打开信息窗体
              //e.target就是被点击的Marker
          }
          let marker = new AMap.Marker({
              position: [116.481181, 39.989792]
          })

          marker.on('click',onMarkerClick);//绑定click事件
          AMap.plugin(['AMap.ToolBar', 'AMap.Scale'], function () {
              map.addControl(new AMap.ToolBar())
              map.addControl(new AMap.Scale())
          })
          map.add(marker);
      }
  },
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
}
</script>

<style lang="less">
  @import "./style/index.less";
</style>
