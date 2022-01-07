<template>
  <div>
    <label
      :for="attrName"
    >
      {{ label }}
    </label>
    <input 
      v-bind="$attrs"
      :id="attrName" 
      :name="attrName"
      :value="modelValue"
      @input="handleInput"
    >
    <slot />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  inheritAttrs: false,
  props: {
    label: {
      type: String,
      required: true
    },
    attrName: {
      type: String,
      required: true
    },
    modelValue: {
      type: [String, Number],
      default: ''
    }
  },
  setup(props, { emit }) {
    const handleInput = (event: Event) => {
      emit('update:modelValue', (event.target as HTMLTextAreaElement).value)
    }

    return {
      handleInput
    }
  },
})
</script>
