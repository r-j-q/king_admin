<template>
    <div class="minheight" :style="{ backgroundImage: 'url(' + login_center_bg + ')' }">
      
    </div>
  </template>
  
  <script>
  import { isvalidUsername } from '@/utils/validate';
  import { setSupport, getSupport, setCookie, getCookie } from '@/utils/support';
  import login_center_bg from '@/assets/images/login_center_bg.png'
  export default {
    name: 'login',
    data() {
      const validateUsername = (rule, value, callback) => {
        if (!isvalidUsername(value)) {
          callback(new Error('请输入正确的用户名'))
        } else {
          callback()
        }
      };
      const validatePass = (rule, value, callback) => {
        if (value.length < 3) {
          callback(new Error('密码不能小于3位'))
        } else {
          callback()
        }
      };
      return {
        loginForm: {
          username: '19138984495',
          password: 'macro123',
        },
        loginRules: {
          username: [{ required: true, trigger: 'blur', validator: validateUsername }],
          password: [{ required: true, trigger: 'blur', validator: validatePass }]
        },
        loading: false,
        pwdType: 'password',
        login_center_bg,
        dialogVisible: false,
        supportDialogVisible: false,
        logo: require('../../../static/logo.png')
      }
    },
    created() { 
    },
    methods: { 
    }
  }
  </script>
  
  <style scoped>
  .minheight {
    
    background: #409EFF;
  
  }
   
  </style>
  