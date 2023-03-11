<template>
  <div class="wrapper">
    <img
      src="http://www.dell-lee.com/imgs/vue3/user.png"
      class="wrapper__img"
    />
    <div class="wrapper__input">
      <input
        class="wrapper__input__content"
        placeholder="用户名"
        v-model="username"
      />
    </div>
    <div class="wrapper__input">
      <input
        type="password"
        class="wrapper__input__content"
        placeholder="请输入密码"
        v-model="password"
         autocomplete="new-password"
      />
    </div>
    <div class="wrapper__login-button" @click="handleLogin">登录</div>
    <div class="wrapper__login-link" @click="handleClick">立即注册</div>
    <Toast v-if="show" :message="toastMessage"  />
  </div>
</template>

<script>
import { useRouter } from "vue-router";
import { post } from "../../utils/request";
import { reactive, toRefs } from "vue";
import Toast,{ useToastEffect } from '../../components/Toast.vue';
 
const useLoginEffect = () => {
  const router = useRouter()
  const data = reactive({ username: '', password: '' })

  const handleLogin = async () => {
    try {
      const result = await post('/api/user/login', {
        username: data.username,
        password: data.password
      })
      if (result?.errno === 0) {
        localStorage.isLogin = true
        router.push({ name: 'Home' })
      } else {
        alert('登陆失败')
      }
    } catch (e) {
      alert('请求失败')
    }
  }

  const { username, password } = toRefs(data)
  return { username, password, handleLogin}
}

// 处理注册跳转
const useRegisterEffect = () => {
  const router = useRouter()
  const handleClick = () => {
    router.push({ name: 'Register' })
  }
  return { handleClick }
}

export default {
  name: 'Login',
  components: { Toast },
  // 职责就是告诉你，代码执行的一个流程
  setup () {
    const { show, toastMessage,  } = useToastEffect()
    const { username, password, handleLogin } = useLoginEffect()
    const { handleClick } = useRegisterEffect()

    return {
      username, password, show, toastMessage,
      handleLogin, handleClick,
    }
  }
}
</script>
<style lang="scss" scoped>
.wrapper {
  position: absolute;
  top: 50%;
  left: 0;
  right: 0;
  transform: translateY(-50%);
  &__img {
    display: block;
    margin: 0 auto 40px auto;
    width: 66px;
    height: 66px;
  }
  &__input {
    height: 48px;
    margin: 0 40px 16px 40px;
    padding: 0 16px;
    background: #f9f9f9;
    border: 1px solid rgba(0, 0, 0, 0.1);
    border-radius: 6px;
    &__content {
      line-height: 48px;
      border: none;
      outline: none;
      width: 100%;
      background: none;
      font-size: 16px;
      color: #777;
      &::placeholder {
        color: #777;
      }
    }
  }
  &__login-button {
    margin: 32px 40px 16px 40px;
    line-height: 48px;
    background: #0091ff;
    box-shadow: 0 4px 8px 0 rgba(0, 145, 255, 0.32);
    border-radius: 4px;
    border-radius: 4px;
    color: #fff;
    font-size: 16px;
    text-align: center;
  }
  &__login-link {
    font-size: 14px;
    color: #777;
    text-align: center;
  }
}
</style> 