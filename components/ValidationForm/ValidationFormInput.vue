<template>
  <div>
    <label :for="labelId">{{ labelName }}</label>
    <input
      :id="labelId"
      v-model="value"
      type="inputType"
      :placeholder="placeHolder"
    />
    <br />
    <span class="error">{{ errorMessage }}</span>
  </div>
</template>
<script lang="ts">
import {
  ref,
  defineComponent,
  watch,
  SetupContext,
  PropType
} from '@vue/composition-api'

import { Domain } from '~/types/index'
export default defineComponent({
  name: 'FormInput',
  props: {
    domainName: {
      type: Function as PropType<Domain>,
      required: true
    },
    labelName: {
      type: String,
      required: true
    },
    labelId: {
      type: String,
      required: true
    },
    inputType: {
      type: String,
      required: true
    },
    placeHolder: {
      type: String,
      required: true
    },
    inputName: {
      type: String,
      required: true
    }
  },
  setup(props, { emit }: SetupContext) {
    const value = ref('')

    const errorMessage = ref('')
    const isValid = ref(false)

    watch(
      value,
      () => {
        isValid.value = false
        errorMessage.value = ''
        emit('input', value.value)
        try {
          props.domainName.validation(value.value)
          isValid.value = true
        } catch (e) {
          errorMessage.value = e.message
        }
      },
      { lazy: true }
    )

    return {
      errorMessage,
      value,
      isValid
    }
  }
})
</script>
<style scoped>
.error {
  color: red;
}
</style>
