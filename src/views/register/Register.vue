<template>
  <div class="wrapper">
    <img
      src="http://www.dell-lee.com/imgs/vue3/user.png"
      class="wrapper__img"
    />
    <div class="wrapper__input">
      <input class="wrapper__input__content" placeholder="请输入用户名" v-model="username"/>
    </div>
    <div class="wrapper__input">
      <input
        class="wrapper__input__content"
        placeholder="请输入密码"
        type="password"
         autocomplete="new-password"
         v-model="password"
      />
    </div>
     <div class="wrapper__input">
      <input
        type="password"
        class="wrapper__input__content"
        placeholder="请确认密码"
        v-model="ensurement"
      />
    </div>
    <div class="wrapper__register-button" @click="handleRegister">注册</div>
    <div class="wrapper__register-link" @click="handLoginClick" >已有账号请登录</div>
    <Toast v-if="show" :message="toastMessage"/>
  </div>
</template>

<script>
import { useRouter } from 'vue-router';
import { reactive, toRefs } from 'vue'
import { post } from '../../utils/request'
import Toast, { useToastEffect } from '../../components/Toast.vue'

const useRegisterEffect = () => {
  const router = useRouter()
  const data = reactive({
    username:'',
    password:'',
    ensurement:''
  })

  const handleRegister = async () => {
    try {
      const result = await post('/api/user/register', {
        username: data.username,
        password: data.password
      })
      if (result?.errno === 0) {
        router.push({ name: 'Login' })
      } else {
        alert('注册失败')
      }
    } catch (e) {
      alert('请求失败')
    }
  }

  const { username, password, ensurement } = toRefs(data)
  return { username, password, ensurement, handleRegister}
}

const useLoginEffect = () => {
  const router = useRouter()
  const handLoginClick = () => {
    router.push({ name:'Login' })
  }
  return { handLoginClick }
}

export default {
  name: 'Register',
  components:{ Toast },
  setup(){
    const { show, toastMessage,  } = useToastEffect()
    const { username, password, ensurement, handleRegister} = useRegisterEffect()
    const { handLoginClick } = useLoginEffect()
    return {
      username, password, ensurement, show, toastMessage,
      handleRegister, handLoginClick
    }  
  }
};
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
  &__register-button {
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
  &__register-link {
    font-size: 14px;
    color: #777;
    text-align: center;
  }
}
</style> 