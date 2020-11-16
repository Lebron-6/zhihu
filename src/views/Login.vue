<template>
  <ValidateForm @form-submit="onFormSubmit">
    <div class="mb-3">
      <label for="exampleInputEmail1" class="form-label">邮箱地址</label>
      <ValidateInput
        :rules="emailRules"
        type="email"
        v-model="emailVal"
        placeholder="请输入邮箱地址"
        ref="inputRef"
      ></ValidateInput>
    </div>
    <div class="mb-3">
      <label for="exampleInputPassword1" class="form-label">密码</label>
      <ValidateInput
        :rules="passwordRules"
        type="password"
        v-model="passwordVal"
        placeholder="请输入密码"
      ></ValidateInput>
    </div>
    <template v-slot:submit>
      <span class="btn btn-danger">SUBMIT</span>
    </template>
  </ValidateForm>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'
import { useRouter } from 'vue-router'
// useRouter 定义路由的行为
// useRoute 获取路由信息
import { useStore } from 'vuex'
import ValidateInput, { RulesProp } from '../components/ValidateInput.vue'
import ValidateForm from '../components/ValidateForm.vue'

export default defineComponent({
  name: 'Login',
  components: {
    ValidateInput,
    ValidateForm
  },
  setup () {
    const store = useStore()
    const emailVal = ref('')
    const router = useRouter()
    const emailRules: RulesProp = [
      { type: 'required', message: '电子邮箱地址不能为空' },
      { type: 'email', message: '请输入正确的电子邮箱' }
    ]
    const passwordVal = ref('')
    const passwordRules: RulesProp = [
      { type: 'required', message: '密码不能为空' }
    ]
    const onFormSubmit = (result: boolean) => {
      // console.log('jisoo', result)
      if (result) {
        router.push('/')
        store.commit('login')
      }
    }
    return {
      emailRules,
      emailVal,
      passwordRules,
      passwordVal,
      onFormSubmit
    }
  }
})
</script>

<style>

</style>
