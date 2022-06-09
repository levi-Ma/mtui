<script lang="ts" setup>
const show = ref(true)
const handelBadgeChange = () => {
  show.value = !show.value
}
</script>

<template>
  <div class="p-4 page-container">
    <div class="p-4 mb-8 rounded-lg module-wrap">
      <div class="title">Badge 徽标数</div>
      <div class="grid grid-rows-1 module-list">
        <div class="module-item">
          <div class="my-2 tit">基本用法</div>
          <div class="flex items-center justify-start" style="gap: 30rpx">
            <mt-badge value="999">
              <mt-image src="example.png" width="100" height="100"></mt-image>
            </mt-badge>
            <mt-badge dot>
              <mt-image src="example.png" width="100" height="100"></mt-image>
            </mt-badge>
          </div>
        </div>
        <div class="module-item">
          <div class="my-2 tit">标记最大数来处理溢出情况</div>
          <div class="my-2 txt">设定 max 来处理溢出情况。</div>
          <div class="flex items-center justify-start" style="gap: 30rpx">
            <mt-badge value="999" :max="15">
              <mt-image src="example.png" width="100" height="100"></mt-image>
            </mt-badge>
          </div>
        </div>
        <div class="module-item">
          <div class="my-2 tit">类型</div>
          <div class="my-2 txt">标记显示类型 'default' | 'success' | 'error' | 'warning' | 'info'</div>
          <div class="flex items-center flex-wrap justify-start" style="gap: 30rpx">
            <mt-badge dot type="default">
              <mt-image src="example.png" width="100" height="100"></mt-image>
            </mt-badge>
            <mt-badge dot type="success">
              <mt-image src="example.png" width="100" height="100"></mt-image>
            </mt-badge>
            <mt-badge dot type="error">
              <mt-image src="example.png" width="100" height="100"></mt-image>
            </mt-badge>
            <mt-badge dot type="warning">
              <mt-image src="example.png" width="100" height="100"></mt-image>
            </mt-badge>
            <mt-badge dot type="info">
              <mt-image src="example.png" width="100" height="100"></mt-image>
            </mt-badge>
          </div>
        </div>
        <div class="module-item">
          <div class="my-2 tit">设置标记的颜色</div>
          <div class="flex items-center justify-start" style="gap: 30rpx">
            <mt-badge value="999" color="#333">
              <mt-image src="example.png" width="100" height="100"></mt-image>
            </mt-badge>
          </div>
        </div>
        <div class="module-item">
          <div class="my-2 tit">设置标记受控显示</div>
          <div class="flex items-center justify-start" style="gap: 30rpx">
            <mt-badge value="999" :show="show">
              <mt-image src="example.png" width="100" height="100"></mt-image>
            </mt-badge>
            <mt-badge dot :show="show">
              <mt-image src="example.png" width="100" height="100"></mt-image>
            </mt-badge>
            <switch :checked="show" @change="handelBadgeChange" />
          </div>
        </div>
        <div class="module-item">
          <div class="my-2 tit">设置标记为 0 时是否显示</div>
          <div class="my-2 txt">设定 show-zero 来显示 0</div>
          <div class="flex items-center justify-start" style="gap: 30rpx">
            <mt-badge value="0" :show-zero="false">
              <mt-image src="example.png" width="100" height="100"></mt-image>
            </mt-badge>
            <mt-badge value="0">
              <mt-image src="example.png" width="100" height="100"></mt-image>
            </mt-badge>
          </div>
        </div>
        <div class="module-item">
          <div class="my-2 tit">设置标记显示进度</div>
          <div class="my-2 txt">设定 processing 来表明正在处理</div>
          <div class="flex items-center justify-start" style="gap: 30rpx">
            <mt-badge dot processing>
              <mt-image src="example.png" width="100" height="100"></mt-image>
            </mt-badge>
            <mt-badge value="0" processing>
              <mt-image src="example.png" width="100" height="100"></mt-image>
            </mt-badge>
            <mt-badge dot type="success" processing>
              <mt-image src="example.png" width="100" height="100"></mt-image>
            </mt-badge>
          </div>
        </div>
      </div>
    </div>
  </div>
  <!-- <div class="p-4">
    <mt-badge value="999">
      <mt-image src="example.png" width="200" height="200"></mt-image>
    </mt-badge>
    <br />
    <br />
    <br />
    <mt-badge value="999"></mt-badge>
  </div> -->
</template>

<style lang="scss" scoped>
.tit {
  font-size: 24rpx;
  color: #000;
}
</style>
