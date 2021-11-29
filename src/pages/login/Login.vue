<template>
  <div>用户名:{{ mainStore.name }}<br />长度:{{ mainStore.nameLength }}</div>
  <hr />
  <button @click="updateName">修改store中的name</button>
</template>

<script setup lang="ts">
import { useMainStore } from '@/store/mian'

const mainStore = useMainStore()

const updateName = () => {
  mainStore.$patch({
    name: '名称被修改了,nameLength也随之改变了',
  })
}
</script>
