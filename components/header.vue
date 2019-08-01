<template>
  <header class="header">
    <el-row type="flex"
            justify="space-between"
            class="main">
      <!-- logo -->
      <div class="logo">
        <nuxt-link to="/">
          <img src="http://157.122.54.189:9093/images/logo.jpg"
               alt="">
        </nuxt-link>
      </div>

      <!-- tab栏 -->
      <el-row type="flex"
              class="navs">
        <nuxt-link to="/">首页</nuxt-link>
        <nuxt-link to="/post">旅游攻略</nuxt-link>
        <nuxt-link to="/hotel">酒店</nuxt-link>
        <nuxt-link to="/air">国内机票</nuxt-link>
      </el-row>

      <!-- 登录信息 -->
      <div v-if="!$store.state.user.userInfo.token">
        <nuxt-link to="/user/login">登录注册</nuxt-link>
      </div>
      <!-- 登录后的布局 -->
      <div v-else>
        <el-dropdown>
          <span class="el-dropdown-link">
            <img src="http://157.122.54.189:9095/assets/images/avatar.jpg"
                 alt="">
            {{$store.state.user.userInfo.user.nickname}}
            <i class="el-icon-arrow-down el-icon--right"></i>
          </span>
          <el-dropdown-menu slot="dropdown">
            <el-dropdown-item>
              <nuxt-link to="#">
                个人中心
              </nuxt-link>
            </el-dropdown-item>
            <el-dropdown-item @click.native="handleLogout">
                退出
            </el-dropdown-item>
          </el-dropdown-menu>
        </el-dropdown>
      </div>

    </el-row>

  </header>
</template>
<script >
export default {
  mounted(){
    
  },
  methods:{
    handleLogout(){
      // console.log("退出");
      this.$store.commit("user/cleanUserInfo")
    }
  }
}
</script>

<style scoped lang='less'>
.header {
  height: 60px;
  line-height: 60px;
  border-bottom: 1px solid #ccc;
  box-shadow: 0 3px 3px #eee;
}
.main {
  width: 1000px;
  margin: 0 auto;
}
.logo {
  margin-top: 8px;
  img {
    width: 156px;
    display: block;
  }
}
.navs {
  height: 60px;
  //   line-height: 60px;
  flex: 1;
  box-sizing: border-box;
  margin-left: 20px;
  a {
    display: block;
    padding: 0 20px;
    &:hover {
      color: #3f9cfe;
      border-bottom: 5px solid #3f9cfe;
    }
  }
  .nuxt-link-exact-active {
    background: #3f9cfe;
    color: #fff;
    &:hover {
      color: #fff;
    }
  }
}
.el-dropdown-link {
  img {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    box-sizing: border-box;
    vertical-align: middle;
    &:hover {
      border: 2px solid #3f9cfe;
    }
  }
}
</style>