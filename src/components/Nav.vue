<template>
  <div class="container">
    <el-container class="mainZone">
      <el-aside width="200px" style="height:100%">
        <el-menu
          :router="true"
          class="el-menu-vertical-demo"
          background-color="#545c64"
          text-color="#fff"
          style="text-align:left;"
          @open="handleOpen"
          @close="handleClose">
          <el-button size="mini" class="m5" type="info" @click="logout">登出</el-button>
          <el-button size="mini" class="m5" type="primary" @click="goChatroom">即時通訊</el-button>
          <el-submenu index="1">
            <template slot="title">
              <i class="el-icon-location"/>
              <span slot="title">用戶管理</span>
            </template>
            <el-menu-item index="1-1" route="/userManager">用戶名單</el-menu-item>
            <el-menu-item index="1-2" route="/loginRecord">登入紀錄</el-menu-item>
            <el-menu-item index="1-3" route="/onlineMember">在線會員</el-menu-item>
          </el-submenu>
          <el-submenu index="2">
            <template slot="title">
              <i class="el-icon-location"/>
              <span slot="title">店家管理</span>
            </template>
            <el-menu-item index="2-1" route="/orderManage">店家訂單</el-menu-item>
            <el-menu-item index="2-2" route="/">選項二</el-menu-item>
          </el-submenu>
        </el-menu>
      </el-aside>
      <el-main class="mainArea">
        <div v-if="getPageName !== '首頁'">
          <el-page-header :content="getPageName" @back="goBack"/>
          <router-view />
        </div>
        <div v-if="getPageName === '首頁'">
          <h1>歡迎來到訂便當系統首頁</h1>
        </div>
        <div class="topBtn placeholder_666"/>
      </el-main>
    </el-container>
  </div>
</template>

<script>
export default {
  data () {
    return {
      pageName:''
    }
  },
  computed:{
    getPageName() {
      return this.$route.name
    }
  },
  created() {
  },
  methods: {
    handleOpen () {

    },
    handleClose () {
      // do nothing
    },
    goBack() {
      this.$router.push("/")
    },
    logout() {
      var url = '/user/logout'
      this.$store.dispatch('Get', url).then(res => {
        this.$message({
          type: 'info',
          message: res.msg
        })
        this.$router.push("/login")
      })
    },
    goChatroom() {
      this.$router.push("/chatroom")
    },
    showWindowInfo () {
      var iw = window.innerWidth
      var ow = window.outerWidth
      var ih = window.innerHeight
      var oh = window.outerHeight
      var str = iw + '-' + ow + '-' + ih + '-' + oh
      this.$message({
        type: 'info',
        message: str
      })
    }
  }
}
</script>

<style>
  .mainZone {
    height: 100%;
  }
  .mt5 {
    margin-top: 5px;
  }
  .mt10 {
    margin-top: 10px;
  }
  .mb5 {
    margin-bottom: 5px;
  }
  .m5 {
    margin: 5px;
  }
  .m10 {
    margin: 10px;
  }
  .el-menu-vertical-demo:not(.el-menu--collapse) {
    width: 198px;
    min-height: 100% ;
  }
</style>