<template>
  <header class="header">
    <!-- 左侧返回按钮 -->
    <div class="header-button is-left" v-show="isLeft">
      <i class="fa fa-chevron-left"></i>
      <button @click="$router.go(-1)">返回</button>
    </div>
    <!-- 标题 -->
    <h1 class="header-title">{{title}}</h1>
    <!-- 右侧图标 -->
    <div class="header-button is-right" v-show="btn_icon">
      <button @click="$emit('rightClick')">
        <i :class="'fa fa-'+ btn_icon"></i>
      </button>
    </div>
  </header>
</template>

<script>
export default {
  name: "Hader",
  props: {
    title: String,
    isLeft: {
      type: Boolean,
      default: false
    },
    btn_icon: String
  }
};
</script>

<style scoped>
.header {
  align-items: center;
  background-color: #009eef;
  box-sizing: border-box;
  color: #fff;
  display: flex;
  font-size: 16px;
  height: 45px;
  line-height: 1;
  padding: 0 10px;
  position: relative;
  text-align: center;
  white-space: nowrap;
  position: fixed;
  width: 100%;
  top: 0;
  z-index: 99;
}

.header-button button {
  background-color: transparent;
  border: 0;
  box-shadow: none;
  color: inherit;
  display: inline-block;
  padding: 0;
  font-size: inherit;
  outline: none;
}
.header-title {
  flex: 1;
  font-size: 16px;
  font-weight:550;
}
.is-left {
  text-align: left;
}
.is-right {
  text-align: right;
}
</style>