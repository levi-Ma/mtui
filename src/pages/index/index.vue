<script lang="ts" setup>
const list = ref([
  { id: 1, title: 'Icon 图标', url: '/pakeage-components/pages/icon' },
  { id: 2, title: 'Image 图片', url: '' },
  { id: 3, title: 'Button 按钮', url: '' },
  { id: 4, title: 'Cell 单元格', url: '' },
  { id: 5, title: 'Badge 徽标数', url: '' },
  { id: 6, title: 'Tag 标签', url: '' },
  { id: 7, title: 'Avatar 头像', url: '' }
])

const handelToModule = (url: string) => {
  url && navigateTo(url)
}
</script>

<template>
  <div class="p-4 page-container">
    <div v-for="item in list" :key="item.id" @click="handelToModule(item.url)">{{ item.title }}</div>
  </div>
</template>

<style lang="scss" scoped></style>
