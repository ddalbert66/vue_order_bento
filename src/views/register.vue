<template>
  <div class="container middle">
    <div class="header">
      <h1>註冊頁面</h1>
    </div>
    <div class="main">
      帳號: <el-input v-model="account" placeholder="請輸入帳號" class="w230 mt5"/><br>
      密碼: <el-input v-model="password" type="password" class="w230 mt5" /><br>
      <el-button class="mt5" @click="register">註冊</el-button>
      <el-button class="mt5" @click="back">回登入頁面</el-button><br>
      <!-- <el-button class="mt5" @click="abc">測試用按鈕</el-button> -->
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      account: '',
      password: ''
    }
  },
  methods: {
    register () {
      var postData = {
        'url': '/user/register',
        'data': {
          'name': this.account,
          'password': this.password
        }
      }
      this.$store.dispatch('Post', postData).then(res => {
        this.$message({
          type: 'info',
          message: res.msg
        })
        this.$router.push("/login")
      })
    },
    back() {
      this.$router.push("/login")
    }
  }
}
</script>

<style>
    .middle {
        width: 100%;
        text-align: center;
    }
    .main {
        /* width: 200px; */
        /* text-align: center; */
        align-content: center;
    }
    .mt5 {
        margin-top: 5px;
    }
    .w230 {
        width: 230px;
    }
</style>
