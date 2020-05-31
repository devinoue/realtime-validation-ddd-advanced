<template>
  <div><slot :isValid="isValid"></slot></div>
</template>
<script lang="ts">
import Vue from 'vue'
import { defineComponent, computed } from '@vue/composition-api'
type Props = {
  observer: any
}
interface ValidationVue extends Vue {
  isValid: boolean
}
export default defineComponent({
  name: '',
  props: {
    observer: {
      type: Object,
      required: false
    }
  },
  setup(props: Props) {
    const isValid = computed(() => {
      return (
        props.observer?.$children.every((component: ValidationVue) => {
          return component?.isValid ?? false
        }) ?? false
      )
    })

    return { isValid }
  }
})
</script>
<style lang="scss" scoped></style>
