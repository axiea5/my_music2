<template>
  <section class="app-main">
    <!-- 左侧导航 -->
    <div class="leftBar">
      <div v-for="(item,index) in list" :key="item.url" class="list-item" :class="key===item.url&&'currentItem'" @click="clickItem(index,item.url)">
        <i class="iconfont" :class="item.icon" />
        <span>{{ item.text }}</span>
      </div>
    </div>
    <transition name="fade-transform" mode="out-in">
      <router-view :key="key" />
    </transition>
  </section>
</template>

<script>
export default {
  name: 'AppMain',
  data() {
    return {
      list: [
        { icon: 'icon-bendi', text: '本地音乐', url: '/local_music' },
        { icon: 'icon-vynil', text: '发现音乐', url: '/find_music' },
        { icon: 'icon-shoucang', text: '我的收藏', url: '/collect_music' },
        { icon: 'icon-bofanggedan', text: '我的歌单', url: '/list_music' },
        { icon: 'icon-xiazai', text: '下载管理', url: '/load_music' }
      ],
      key: 1
    }
  },
  watch: {
    '$route': function(newUrl, oldUrl) {
      this.key = new Date().getTime()
    }
  },
  methods: {
    clickItem(index, url) {
      this.$router.push(url)
    }
  }
}
</script>

<style lang="less" scoped>
@import "~@/styles/iconfont.css";
.icon {
  width: 1em;
  height: 1em;
  vertical-align: -0.15em;
  fill: currentColor;
  overflow: hidden;
}
.app-main {
  /*80 = navbar  */
  height: calc(100vh - 140px);
  position: relative;
  overflow: hidden;
  display: flex;
  .leftBar {
    width: 200px;
    height: 100%;
    border-right: 1px solid #ccc;
    padding-top: 10px;
    .list-item {
      padding: 10px 15px 10px;
      color: #303030;
      cursor: pointer;
      i {
        margin-right: 8px;
      }
      &:hover {
        background: #efefef;
      }
    }
    .currentItem {
      background: #efefef;
      font-weight: bold;
    }
  }
}
</style>
