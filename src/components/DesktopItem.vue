<template>
  <div class="desktop-item" :class="{
                                       selected:selected,
                                       dragging:dragging
                                       }">
    <div class="item-body" @mousedown="onMouseDown" @dblclick="onDbClick">
      <div class="icon" :style="{
                                         'background-image':'url(' + icon + ')'
                                         }">

      </div>
      <div class="text">
        {{item.Name}}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['item', 'dragging', 'selected'],
  computed: {
    icon () {
      // console.log('item Icon', this.item.Icon)
      let upFileName = this.item.Name
      let index1 = upFileName.lastIndexOf('.')
      let index2 = upFileName.length
      let suffix = upFileName.substring(index1 + 1, index2) // 后缀名
      return 'http://localhost:8000/file-icons/' + suffix + '.png'
    }
  },
  methods: {
    onMouseDown () {

    },
    onDbClick () {
      this.$engine.call({
        Service: 'ZeroRoo.DefaultApp.Services.Open',
        Data: this.item.Target
      })
    }
  }
}
</script>

<style lang="less" scoped>
.desktop-item {
  // position: absolute;
  /*border:1px dashed #fff;*/
  margin: 5px;
  width: 90px;
  height: 100px;
  &:hover {
    background: rgba(0, 134, 255, 0.27);
  }
  &.selected {
    .item-body {
      /*border:2px solid rgba(43, 115, 199, 0.36);*/
      /*background:rgba(43, 115, 199, 0.2);*/
      background: rgba(0, 134, 255, 0.27);
    }
  }
  &.dragging {
    opacity: 0.6;
  }
  .item-body {
    /*border:2px solid transparent;*/
    border-radius: 4px; // position: absolute;
    top: 50%;
    left: 50%;
    .icon {
      height: 80px;
      width: 64px;
      margin: 0 auto;
      background-size: 64px;
      background-repeat: no-repeat;
      background-position-y: 8px;
    }
    .text {
      min-height: 20px;
      line-height: 20px;
      height: 20px;
      text-align: center;
      /*margin:0 -10px; */
      display: block;
      overflow: hidden;
      word-wrap: break-word;
      word-break: break-all;
      text-overflow: hiden;
      padding-bottom: 5px;
      cursor: default;
    }
  }
}
</style>


