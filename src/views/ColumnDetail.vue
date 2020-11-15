<template>
  <!-- <pre>{{ route }}</pre> -->
  <!-- pre标签可以定义预格式化的文本 在pre中文本可以保留空格和换行符 并且文本会显示等宽字体 -->
  <div class="column-detail-page w-75 mx-auto">
    <div class="column-info row mb-4 border-bottom pb-4 align-items-center">
      <div class="col-3 text-center">
        <img :src="column.avatar" :alt="column.title" class="rounded-circle border w-100">
      </div>
      <div class="col-9">
        <h4>{{ column.title }}</h4>
        <p class="text-muted">{{ column.description }}</p>
      </div>
    </div>
    <PostList :list="list"></PostList>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { useRoute } from 'vue-router'
import { testData, testPosts } from '../testData'
import PostList from '../components/PostList.vue'

export default defineComponent({
  components: {
    PostList
  },
  setup () {
    const route = useRoute()
    const currentId = +route.params.id
    // + 字符串转number格式
    const column = testData.find(c => c.id === currentId)
    const list = testPosts.filter(post => post.columnId === currentId)
    return {
      route,
      column,
      list
    }
  }
})
</script>

<style>

</style>
