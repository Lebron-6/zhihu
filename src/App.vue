<template>
  <div class="container">
    <GlobalHeader :user="currentUser" />
    <ColumnList :list="list" />
    <ValidateForm @form-submit="onFormSubmit">
      <div class="mb-3">
        <label for="exampleInputEmail1" class="form-label">邮箱地址</label>
        <!-- <input
          type="email"
          class="form-control"
          id="exampleInputEmail1"
          v-model="emailRef.val"
          @blur="validateEmail"
        /> -->
        <ValidateInput
          :rules="emailRules"
          type="email"
          v-model="emailVal"
          placeholder="请输入邮箱地址"
          ref="inputRef"
        ></ValidateInput>
        <!-- <h1>{{ emailVal }}</h1> -->
        <!-- <div v-if="emailRef.error" class="form-text">{{ emailRef.message }}</div> -->
      </div>
      <div class="mb-3">
        <label for="exampleInputPassword1" class="form-label">密码</label>
        <!-- <input type="password" class="form-control" id="exampleInputPassword1"> -->
        <ValidateInput
          :rules="passwordRules"
          type="password"
          v-model="passwordVal"
          placeholder="请输入密码"
        ></ValidateInput>
      </div>
      <!-- <div class="mb-3 form-check">
        <input type="checkbox" class="form-check-input" id="exampleCheck1">
        <label class="form-check-label" for="exampleCheck1">Check me out</label>
      </div> -->
      <!-- <button type="submit" class="btn btn-primary">Submit</button> -->
      <template v-slot:submit>
        <!-- 具名插槽缩写 v-slot: 替换为字符 # -->
        <span class="btn btn-danger">SUBMIT</span>
      </template>
    </ValidateForm>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, ref } from 'vue'
import 'bootstrap/dist/css/bootstrap.min.css'
import ColumnList, { ColumnProps } from './components/ColumnList.vue'
import GlobalHeader, { UserProps } from './components/GlobalHeader.vue'
import ValidateInput, { RulesProp } from './components/ValidateInput.vue'
import ValidateForm from './components/ValidateForm.vue'

const currentUser: UserProps = {
  isLogin: true,
  name: 'jisoo'
}

const testData: ColumnProps[] = []

// const testData: ColumnProps[] = [
//   {
//     id: 1,
//     title: 'blackpink',
//     description: 'ROSE LISA JISOO JENNIE',
//     avatar: 'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1605300503769&di=4b5409d0554c66bf544af9abf2fd22c4&imgtype=0&src=http%3A%2F%2Fc-ssl.duitang.com%2Fuploads%2Fitem%2F202002%2F04%2F20200204143739_dxgbs.thumb.400_0.jpg'
//   },
//   {
//     id: 2,
//     title: 'blackpink',
//     description: 'ROSE LISA JISOO JENNIE'
//     // avatar: 'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1605300503769&di=4b5409d0554c66bf544af9abf2fd22c4&imgtype=0&src=http%3A%2F%2Fc-ssl.duitang.com%2Fuploads%2Fitem%2F202002%2F04%2F20200204143739_dxgbs.thumb.400_0.jpg'
//   },
//   {
//     id: 3,
//     title: 'blackpink',
//     description: 'ROSE LISA JISOO JENNIE',
//     avatar: 'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1605300503769&di=4b5409d0554c66bf544af9abf2fd22c4&imgtype=0&src=http%3A%2F%2Fc-ssl.duitang.com%2Fuploads%2Fitem%2F202002%2F04%2F20200204143739_dxgbs.thumb.400_0.jpg'
//   },
//   {
//     id: 4,
//     title: 'blackpink',
//     description: 'ROSE LISA JISOO JENNIE'
//     // avatar: 'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1605300503769&di=4b5409d0554c66bf544af9abf2fd22c4&imgtype=0&src=http%3A%2F%2Fc-ssl.duitang.com%2Fuploads%2Fitem%2F202002%2F04%2F20200204143739_dxgbs.thumb.400_0.jpg'
//   },
//   {
//     id: 5,
//     title: 'blackpink',
//     description: 'ROSE LISA JISOO JENNIE',
//     avatar: 'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1605300503769&di=4b5409d0554c66bf544af9abf2fd22c4&imgtype=0&src=http%3A%2F%2Fc-ssl.duitang.com%2Fuploads%2Fitem%2F202002%2F04%2F20200204143739_dxgbs.thumb.400_0.jpg'
//   },
//   {
//     id: 6,
//     title: 'blackpink',
//     description: 'ROSE LISA JISOO JENNIE',
//     avatar: 'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1605300503769&di=4b5409d0554c66bf544af9abf2fd22c4&imgtype=0&src=http%3A%2F%2Fc-ssl.duitang.com%2Fuploads%2Fitem%2F202002%2F04%2F20200204143739_dxgbs.thumb.400_0.jpg'
//   }
// ]

const emailReg = /^[a-zA-Z0-9.!#$%&’*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$/

export default defineComponent({
  name: 'App',
  components: {
    ColumnList,
    GlobalHeader,
    ValidateInput,
    ValidateForm
  },
  setup () {
    const inputRef = ref()
    const emailVal = ref('')
    const emailRules: RulesProp = [
      { type: 'required', message: '电子邮箱地址不能为空' },
      { type: 'email', message: '请输入正确的电子邮箱' }
    ]
    const passwordVal = ref('')
    const passwordRules: RulesProp = [
      { type: 'required', message: '密码不能为空' }
    ]
    const onFormSubmit = (result: boolean) => {
      console.log('jisoo', result)
      console.log(inputRef.value.validateInput())
    }
    const emailRef = reactive({
      val: '',
      error: false,
      message: ''
    })
    const validateEmail = () => {
      if (emailRef.val.trim() === '') {
        emailRef.error = true
        emailRef.message = '邮箱不能为空!'
      } else if (!emailReg.test(emailRef.val)) {
        emailRef.message = '邮箱格式不正确!'
      }
    }
    return {
      list: testData,
      currentUser,
      emailRef,
      validateEmail,
      emailRules,
      emailVal,
      passwordRules,
      onFormSubmit,
      inputRef,
      passwordVal
    }
  }
})
</script>

<style></style>
