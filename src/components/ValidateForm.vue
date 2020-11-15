<template>
  <form action="" class="validate-form-container">
    <slot name="default"></slot>
    <div class="submit-area" @click.prevent="submitForm">
      <slot name="submit">
        <button type="submit" class="btn btn-primary">提交</button>
      </slot>
    </div>
  </form>
</template>

<script lang="ts">
import { defineComponent, onUnmounted } from 'vue'
import mitt from 'mitt'
// 自定义监听器
export const emitter = mitt()

type validateFunc = () => boolean
// 可以返回一个包含错误信息的对象

export default defineComponent({
  emits: ['form-submit'],
  setup (props, context) {
    let funcArr: validateFunc[] = []
    const submitForm = () => {
      // const result = funcArr.every(func => func())
      // 当使用every,循环中出现false时,循环中断返回false
      const result = funcArr.map(func => func()).every(result => result)
      context.emit('form-submit', result)
    }
    const callback = (func: validateFunc) => {
      funcArr.push(func)
    }
    emitter.on('form-item-created', callback)
    onUnmounted(() => {
      emitter.off('form-item-created', callback)
      funcArr = []
    })
    return {
      submitForm
    }
  }
})
</script>

<style>

</style>
