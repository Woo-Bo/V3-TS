<script setup lang="ts">
import v from '@/plugins/validate'
import utils from '@/utils'

const { yup, useForm, useField, useFields } = v

const schema = {
  account: yup
    .string()
    .required()
    .matches(/^\d{11}|.+@.+$/, '请输入邮箱或手机号')
    .label('帐号'),
  password: yup.string().required().min(3, '密码不能少于3位').label('密码'),
}

const { handleSubmit, errors, values } = useForm({
  initialValues: {
    account: '2300071698@qq.com',
    password: 'admin888',
  },
  validationSchema: schema,
})
useFields(Object.keys(schema))

const onSubmit = handleSubmit(async (values: any) => {
  utils.user.login(values)
})
</script>

<template>
  <form class @submit="onSubmit">
    <div
      class="w-[720px] translate-y-32 md:translate-y-0 bg-white md:grid grid-cols-2 rounded-md shadow-md overflow-hidden">
      <div class="p-6 flex flex-col justify-between">
        <div>
          <h2 class="text-center text-gray-700 text-lg mt-3">会员登录</h2>
          <div class="mt-8">
            <HdInput v-model="values.account" />
            <!-- {{ accountError }} -->
            <HdError :error="errors.account" />

            <HdInput v-model="values.password" class="mt-3" />
            <HdError :error="errors.password" />
            <!-- {{ passwordError }} -->
            <!-- <Field
              name="account"
              value="admin@sdklsdklds"
              class="hd-input"
              label="帐号"
              placeholder="请输入邮箱或手机号" />
            <div v-if="errors.account" class="hd-error">请输入邮箱或手机号</div> -->
            <!-- <Field
              name="password"
              value="admin888"
              class="hd-input mt-3"
              label="密码"
              type="password"
              placeholder="请输入登录密码" />
            <ErrorMessage name="password" as="div" class="hd-error" /> -->
          </div>

          <HdButton class="w-full" />
          <div class="flex justify-center mt-3">
            <icon-wechat
              theme="outline"
              size="24"
              fill="#fff"
              class="fab fa-weixin bg-green-600 text-white rounded-full p-1 cursor-pointer" />
            <!-- <i ></i> -->
          </div>
        </div>
        <div class="flex gap-2 justify-center mt-5">
          <a href="#" class="text-xs text-gray-700">会员注册</a>
          <a href="#" class="text-xs text-gray-700">找回密码</a>
          <a href="#" class="text-xs text-gray-700">找回密码</a>
        </div>
      </div>
      <div class="hidden md:block relative">
        <img src="/images/login.jpg" class="absolute h-full w-full object-cover" />
      </div>
    </div>
  </form>
</template>

<style lang="scss">
form {
  @apply bg-slate-300 h-screen flex justify-center items-start md:items-center p-5;
}
</style>
