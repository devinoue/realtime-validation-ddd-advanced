<template>
  <div class="container">
    <ValidationObserver
      ref="observer"
      v-slot="{ isValid }"
      :observer="observer"
    >
      <FormInput
        v-model="forms.name"
        :domain-name="Name"
        :label-id="'name'"
        :label-name="'名前'"
        :input-type="'text'"
        :input-name="'name'"
        :place-holder="'名前を入力してください'"
      />
      <FormInput
        v-model="forms.email"
        :domain-name="EmailAddress"
        :label-id="'email'"
        :label-name="'メールアドレス'"
        :input-type="'text'"
        :input-name="'email'"
        :place-holder="'メールアドレスを入力してください'"
      />
      <button :disabled="!isValid">ボタン</button>
    </ValidationObserver>
    {{ forms }}
  </div>
</template>
<script lang="ts">
import { ref, reactive } from '@vue/composition-api'
import Name from '~/domain/Name'
import EmailAddress from '~/domain/EmailAddress'
import FormInput from '~/components/ValidationForm/ValidationFormInput.vue'
import ValidationObserver from '~/components/ValidationForm/ValidationObserver.vue'

export default {
  name: 'Index',
  components: { FormInput, ValidationObserver },
  setup() {
    const observer = ref<any>(null) // 必須
    const forms = reactive({
      name: '',
      email: ''
    })

    return { Name, EmailAddress, forms, observer }
  }
}
</script>
<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  flex-direction: column;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
