<template>
<div>
    <van-nav-bar title="首页"/>
    <van-tabs v-model="activeName">
      <van-tab title="标签 1" name="a">
        <van-pull-refresh v-model="isLoading" @refresh="onRefresh">
        <van-list
          v-model="loading"
          :finished="finished"
          finished-text="没有更多了"
          @load="onLoad"
        >
          <van-cell
            v-for="item in list"
            :key="item"
            :title="item"
          />
        </van-list>
          <p>刷新次数: {{ count }}</p>
        </van-pull-refresh>
      </van-tab>
      <van-tab title="标签 2" name="b">内容 2</van-tab>
      <van-tab title="标签 3" name="c">内容 3</van-tab>
      <van-tab title="标签 4" name="b">内容 4</van-tab>
      <van-tab title="标签 5" name="c">内容 5</van-tab>
      <van-tab title="标签 6" name="b">内容 6</van-tab>
      <van-tab title="标签 7" name="c">内容 7</van-tab>
    </van-tabs>
<!-- 底部导航 -->
    <van-tabbar v-model="active">
    <van-tabbar-item icon="home-o">标签</van-tabbar-item>
    <van-tabbar-item icon="search">标签</van-tabbar-item>
    <van-tabbar-item icon="friends-o">标签</van-tabbar-item>
    <van-tabbar-item icon="setting-o">标签</van-tabbar-item>
  </van-tabbar>
</div>
</template>

<script>
export default {
  name: 'home',
  data () {
    return {
      active: 0,
      activeName: 'a',
      list: [],
      loading: false,
      finished: false,
      count: 0,
      isLoading: false
    }
  },
  methods: {
    onLoad () {
      // 异步更新数据
      setTimeout(() => {
        for (let i = 0; i < 10; i++) {
          this.list.push(this.list.length + 1)
        }
        // 加载状态结束
        this.loading = false

        // 数据全部加载完成
        if (this.list.length >= 40) {
          this.finished = true
        }
      }, 500)
    },
    onRefresh () {
      setTimeout(() => {
        this.$toast('刷新成功')
        this.isLoading = false
        this.count++
      }, 500)
    }
  }
}

</script>

<style>

</style>
