<script lang="ts" setup>
const btnClick = (e: Event) => {
  showToast({
    title: '点击了按钮'
  })
}
</script>
<template>
  <div class="p-4 page-container">
    <div class="p-4 rounded-lg module-wrap">
      <div class="title">Button 按钮</div>
      <div class="grid grid-rows-1 module-list">
        <div class="module-item">
          <div class="my-2 tit">基本用法</div>
          <mt-button @click="btnClick">基本用法</mt-button>
        </div>
        <div class="module-item">
          <div class="my-2 tit">按钮的预置样式</div>
          <div class="grid grid-cols-1" style="gap: 20rpx">
            <mt-button>default</mt-button>
            <mt-button type="primary">primary</mt-button>
            <mt-button type="error">error</mt-button>
            <mt-button type="warning">warning</mt-button>
            <mt-button type="success">success</mt-button>
          </div>
        </div>
        <div class="module-item">
          <div class="my-2 tit">文本按钮</div>
          <div class="grid grid-cols-1" style="gap: 20rpx">
            <mt-button type="text">
              <mt-icon name="tishi3"></mt-icon>
              文本按钮
            </mt-button>
          </div>
        </div>
        <div class="module-item">
          <div class="my-2 tit">设置按钮尺寸</div>
          <div class="grid grid-cols-1" style="gap: 20rpx">
            <div>
              <mt-button type="primary">默认</mt-button>
            </div>
            <div>
              <mt-button type="primary" size="medium">中等</mt-button>
            </div>
            <div>
              <mt-button type="primary" size="mini">迷你</mt-button>
            </div>
          </div>
        </div>
        <div class="module-item">
          <div class="my-2 tit">设置按钮形状</div>
          <div class="grid grid-cols-1" style="gap: 20rpx">
            <mt-button type="error">矩形</mt-button>
            <mt-button type="error" shape="circle">半圆</mt-button>
            <mt-button type="error" shape="square">圆角</mt-button>
          </div>
        </div>
        <div class="module-item">
          <div class="my-2 tit">设置按钮镂空</div>
          <div class="grid grid-cols-1" style="gap: 20rpx">
            <mt-button plain>default</mt-button>
            <mt-button type="primary" plain>primary</mt-button>
            <mt-button type="error" plain>error</mt-button>
            <mt-button type="warning" plain>warning</mt-button>
            <mt-button type="success" plain>success</mt-button>
          </div>
        </div>
        <div class="module-item">
          <div class="my-2 tit">设置按钮禁止状态</div>
          <div class="grid grid-cols-1" style="gap: 20rpx">
            <mt-button disabled>default</mt-button>
            <mt-button type="primary" disabled>primary</mt-button>
            <mt-button type="error" disabled>error</mt-button>
            <mt-button type="warning" disabled>warning</mt-button>
            <mt-button type="success" disabled>success</mt-button>
          </div>
        </div>
        <div class="module-item">
          <div class="my-2 tit">设置按钮是否加载中</div>
          <div class="grid grid-cols-1" style="gap: 20rpx">
            <mt-button disabled isLoading>default</mt-button>
            <mt-button type="primary" disabled isLoading>primary</mt-button>
            <mt-button type="error" disabled isLoading>error</mt-button>
            <mt-button type="warning" disabled isLoading>warning</mt-button>
            <mt-button type="success" disabled isLoading>success</mt-button>
          </div>
        </div>
        <div class="module-item">
          <div class="my-2 tit">设置按钮节流</div>
          <div class="grid grid-cols-1" style="gap: 20rpx">
            <mt-button @click="btnClick" :throttle-time="5000" type="primary">primary</mt-button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.tit {
  font-size: 24rpx;
  color: #000;
}
</style>
