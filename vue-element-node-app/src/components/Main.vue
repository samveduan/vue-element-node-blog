<template>
  <div id="app">
    <el-container style="height: 100%;">
      <el-header style="height: 80px;" :style="topBg">
        <el-row style="height: 80px;">
          <el-col :span="6" class="logo">
            <img :src="require('../assets/logo.svg')" />Ant Design管理系统
          </el-col>
          <el-col :span="4" style="padding-top: 10px;">
            <el-radio-group v-model="isCollapse" style="margin-bottom: 20px;">
              <el-radio-button :label="false">展开</el-radio-button>
              <el-radio-button :label="true">收起</el-radio-button>
            </el-radio-group>
          </el-col>
          <el-col :span="13" :offset="1">
            <el-dropdown style="float: right;">
              <span class="el-dropdown-link" style="color: #ffffff;">
                user001
                <i class="el-icon-arrow-down el-icon--right"></i>
              </span>
              <el-dropdown-menu slot="dropdown">
                <el-dropdown-item icon="el-icon-edit">修改密码</el-dropdown-item>
                <el-dropdown-item icon="el-icon-setting">设置默认密级</el-dropdown-item>
                <el-dropdown-item icon="el-icon-circle-close" @click.native="loginout()">退出</el-dropdown-item>
              </el-dropdown-menu>
            </el-dropdown>
          </el-col>
        </el-row>
      </el-header>
      <el-container>
        <el-aside width="auto" :style="leftBg">
          <el-row class="tac">
            <el-col :span="24">
              <el-menu
                :default-active="$route.path"
                class="el-menu-vertical-demo"
                @open="handleOpen"
                @close="handleClose"
                background-color="none"
                text-color="#fff"
                active-text-color="#ff0000"
                :unique-opened="true"
                :collapse="isCollapse"
              >
                <template v-for="route in this.$router.options.routes[2].children">
                  <!-- 循环有子目录的菜单 -->
                  <el-submenu
                    :key="route.alias"
                    :index="route.alias"
                    v-if="route.children && route.children.length"
                  >
                    <template slot="title">
                      <i :class="route.meta.icon"></i>
                      <span>{{route.meta.title}}</span>
                    </template>
                    <el-menu-item-group>
                      <router-link
                        :to="subroute.alias"
                        :key="subroute.alias"
                        v-for="subroute in route.children"
                      >
                        <el-menu-item :index="subroute.alias">{{subroute.meta.title}}</el-menu-item>
                      </router-link>
                    </el-menu-item-group>
                  </el-submenu>
                  <!-- 循环有子目录的菜单 -->

                  <!-- 循环没有子目录的菜单 -->
                  <router-link
                    :to="route.alias"
                    :key="route.alias"
                    v-else-if="!route.children && route.alias != '/' && route.alias != '/login'"
                  >
                    <el-menu-item :index="route.alias">
                      <i :class="route.meta.icon"></i>
                      <span slot="title">{{route.meta.title}}</span>
                    </el-menu-item>
                  </router-link>
                  <!-- 循环没有子目录的菜单 -->
                </template>
              </el-menu>
            </el-col>
          </el-row>
        </el-aside>
        <el-main style="padding: 15px;">
          <router-view></router-view>
        </el-main>
      </el-container>
    </el-container>
  </div>
</template>
 
<script>
import Header from "@/components/Header";
export default {
  name: "App",
  data() {
    return {
      isCollapse: true,
      leftBg: {
        background: "#001529"
      },
      topBg: {
        background: "#001529",
        height: "80px",
        fontSize: "32px",
        color: "#ffffff"
      }
      // leftBg: {
      //   background:
      //     "#235d8b url(" +
      //     require("../assets/left-bg.png") +
      //     ") no-repeat scroll 0 bottom"
      // },
      // topBg: {
      //   background:
      //     "#235d8b url(" +
      //     require("../assets/top-bg.png") +
      //     ") no-repeat scroll right 0",
      //   height: "80px",
      //   fontSize: "32px",
      //   color: "#ffffff"
      // }
    };
  },
  components: {
    Header
  },
  methods: {
    handleOpen(key, keyPath) {
      console.log(key, keyPath);
    },
    handleClose(key, keyPath) {
      console.log(key, keyPath);
    }
  }
};
</script>
 
<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  height: 100%;
}

.el-header,
.el-footer {
  background-color: #b3c0d1;
  color: #333;
  line-height: 80px;
}

.logo {
  height: 80px;
  line-height: 80px;
  font-size: 30px;
  font-family: "微软雅黑";
  font-weight: bold;
  text-shadow: 0 0 5px #000000;
  display: flex;
  align-items: center;
}

.logo img {
  margin: 0 5px 0 0;
  width: 35px;
  height: 35px;
}

.el-aside {
  background-color: #d3dce6;
  color: #333;
}

.el-aside a {
  text-decoration: none;
}

.el-menu {
  background: none;
  border-right: 0;
}

.el-submenu__title {
  background: none !important;
}

.el-menu-item-group .el-menu-item {
  padding-left: 52px !important;
}
.el-menu-item {
  background: rgb(0, 21, 41) !important;
}
.el-menu-item.is-active {
  color: #ffffff !important;
  background: #1890ff !important;
}

.el-main {
  background-color: #f0f2f5;
  color: #333;
  padding: 0;
}

body > .el-container {
  margin-bottom: 40px;
}

.el-container:nth-child(5) .el-aside,
.el-container:nth-child(6) .el-aside {
  line-height: 260px;
}

.el-container:nth-child(7) .el-aside {
  line-height: 320px;
}

.el-menu-vertical-demo:not(.el-menu--collapse) {
  width: 200px;
  min-height: 400px;
}
</style>