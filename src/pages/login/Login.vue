<template>
  <div>这是login页面</div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'

export default defineComponent({
  name: 'LoginPage',
  setup() {
    const count = ref(0)

    return { count }
  },
})
</script>
