<template>
  <li class="Dropdowm-item" :class="{'is-disabled':disabled}" @click="itemClick">
    <slot></slot>
  </li>
</template>

<script lang='ts'>
import { defineComponent, onUnmounted, onBeforeUnmount } from 'vue'
// import mitt from 'mitt'// 事件监听器
// export const mitter = mitt()
import mitter from '@/utils/mitt'
export default defineComponent({
  name: 'DropdownItem',
  props: {
    disabled: {
      type: Boolean,
      default: false
    },
    command: {
      type: String,
      default: ''
    }
  },
  components: {},
  setup (props) {
    const itemClick = (event:any) => {
      console.log(event.path[0].className)
      // if (mitter) {
      //   mitter.off('handlerCommand')
      // }

      mitter.emit('handlerCommand', props.command)
      // console.log(mitter.emit('handlerCommand', props.command))
    }

    return {
      itemClick
    }
  }
})
</script>

<style scoped lang='scss'>
.Dropdowm-item.is-disabled{
  color: #c0c4cc;
  pointer-events: none;
  background: transparent;
}
.Dropdowm-item {
  padding: 0px 10px;
  user-select: none;
  text-align: center;
  font-size: 14px;
  line-height: 30px;
  &:hover {
    background: rgba(0, 104, 255, 0.2);
    color: #ffffff;
  }
  &:not(:nth-last-of-type(1)) {
    margin-bottom: 5px;
  }
}
</style>
