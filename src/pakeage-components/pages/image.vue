<script lang="ts" setup>
const url = ref('../../static/image.png')
const errorUrl = ref('https://sponsors.vuejs.org/example/fade.jpg')
</script>

<template>
  <div class="p-4 page-container">
    <div class="p-4 rounded-lg module-wrap">
      <div class="title">Image 图片</div>
      <div class="grid grid-rows-1 module-list">
        <div class="module-item">
          <div class="my-2 tit">基本用法</div>
          <mt-image :src="url" width="160" height="160"></mt-image>
        </div>
        <div class="module-item">
          <div class="my-2 tit">更改图片大小</div>
          <mt-image :src="url" width="200" height="200"></mt-image>
        </div>
        <div class="module-item">
          <div class="my-2 tit">使用父级元素宽高</div>
          <div style="width: 220rpx; height: 220rpx">
            <mt-image :src="url"></mt-image>
          </div>
        </div>
        <div class="module-item">
          <div class="my-2 tit">设置图片形状</div>
          <mt-image :src="url" width="200" height="200" shape="circle"></mt-image>
        </div>
        <div class="module-item">
          <div class="my-2 tit">设置图片圆角</div>
          <mt-image :src="url" width="200" height="200" border-radius="10"></mt-image>
        </div>
        <div class="module-item">
          <div class="my-2 tit">图片加载失败</div>
          <mt-image :src="errorUrl" width="200" height="200"></mt-image>
        </div>
        <div class="module-item">
          <div class="my-2 tit">自定义图片加载失败</div>
          <mt-image :src="errorUrl" width="200" height="200">
            <template #error>
              <mt-icon name="tupian" size="40"></mt-icon>
            </template>
          </mt-image>
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
