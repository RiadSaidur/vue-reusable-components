<template>
  <div
    ref="clickOutsideRef"
  >
    <slot></slot>
  </div>
</template>

<script lang="ts">
import { defineComponent, onMounted, onUnmounted, ref } from 'vue'

export default defineComponent({
  setup(props, { emit }) {
    const clickOutsideRef = ref(null)

    const handler = (event: Event) => {
      const clickedOutsideElement = clickOutsideRef.value as unknown as HTMLElement
      const clickedNode = event.target as Node
      
      if(!clickedOutsideElement.children[0].contains(clickedNode)) emit('clickedOutside')
    }

    onMounted(() => {
      document.addEventListener('mousedown', handler)
    })

    onUnmounted(() => {
      document.removeEventListener('mousedown', handler)
    })

    return {
      clickOutsideRef
    }
  },
})
</script>
