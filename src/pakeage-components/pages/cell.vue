<script lang="ts" setup>
const handelCellItem = (index: string | number) => {
  showToast({
    title: '点击事件'
  })

  console.log(index)
}
</script>

<template>
  <div class="p-4 page-container">
    <div class="p-4 rounded-lg module-wrap">
      <div class="title">Cell 单元格</div>

      <div class="grid grid-rows-1 module-list">
        <div class="module-item">
          <div class="my-2 tit">基本用法</div>
          <mt-cell-item title="单元格" @click="handelCellItem" index="1"></mt-cell-item>
        </div>
        <div class="module-item">
          <div class="my-2 tit">成组使用</div>
          <mt-cell title="成组使用">
            <mt-cell-item title="单元格1"></mt-cell-item>
            <mt-cell-item title="单元格2"></mt-cell-item>
            <mt-cell-item title="单元格3"></mt-cell-item>
          </mt-cell>
        </div>
        <div class="module-item">
          <div class="my-2 tit">开启左右 icon</div>
          <mt-cell-item title="单元格" icon="lianjie" is-arrow></mt-cell-item>
        </div>
        <div class="module-item">
          <div class="my-2 tit">开启描述和右侧文字</div>
          <mt-cell-item title="单元格" label="描述" value="右侧文字"></mt-cell-item>
        </div>
        <div class="module-item">
          <div class="my-2 tit">自定义左右icon</div>
          <mt-cell-item title="单元格">
            <template #leftIcon>
              <mt-icon name="shengyin" size="40" color="red"></mt-icon>
            </template>
          </mt-cell-item>

          <mt-cell-item title="单元格">
            <template #rightIcon>
              <mt-icon name="wenhao" size="40" color="green"></mt-icon>
            </template>
          </mt-cell-item>
        </div>
        <div class="module-item">
          <div class="my-2 tit">自定义右侧内容</div>
          <mt-cell-item title="单元格">
            <template #rightValue> 自定义右侧内容<mt-icon name="wenhao" size="40" color="green"></mt-icon> </template>
          </mt-cell-item>
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
