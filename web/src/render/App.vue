<template>
  <div id="app">
    <router-view></router-view>
  </div>
</template>
<script setup lang="ts">
import { computed, watch } from 'vue'
import { useStore } from 'vuex'
import { get as _get } from 'lodash-es'

const store = useStore()
const skinConf = computed(() => _get(store, 'state.skinConf', {}))

const updateSkinConfig = (value: any) => {
  const root = document.documentElement
  const { themeConf, backgroundConf, contentConf } = value

  if (themeConf?.color) {
    // 设置主题颜色
    root.style.setProperty('--primary-color', themeConf?.color)
  }

  if (backgroundConf?.color) {
    // 设置背景颜色
    root.style.setProperty('--primary-background-color', backgroundConf?.color)
  }

  if (contentConf?.opacity.toString()) {
    // 设置全局透明度
    root.style.setProperty('--opacity', `${parseInt(contentConf.opacity) / 100}`)
  }
}

watch(skinConf, (value) => {
  updateSkinConfig(value)
})
</script>
<style lang="scss">
@import url('./styles/icon.scss');
@import url('../materials/questions/common/css/icon.scss');
@import url('./styles/reset.scss');

html {
  background: #f7f7f7;
}

#app {
  position: relative;
  overflow-x: hidden;
  width: 100%;
  max-width: 750px;
  margin: auto;
  height: 100%;
  display: flex;
  flex-direction: column;
  flex: 1;
  background-color: #fff;
}
</style>
