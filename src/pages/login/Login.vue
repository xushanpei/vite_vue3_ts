<template>
  <div class="test">用户名:{{ mainStore.name }}<br />长度:{{ mainStore.nameLength }}</div>
  <hr />
  <button @click="updateName">修改store中的name</button>
  <hr />

  <n-button>naive-ui</n-button>
</template>

<script setup lang="ts">
import { useMainStore } from '@/store/main'
import { NButton } from 'naive-ui'

const mainStore = useMainStore()

const updateName = () => {
  mainStore.$patch({
    name: '名称被修改了,nameLength也随之改变了',
  })
}
</script>

<style lang="scss" scoped>
.test {
  color: $test-color;
}
</style>
