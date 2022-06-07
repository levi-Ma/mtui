<script lang="ts">
defineComponent({
  name: 'MtIcon',
  inheritAttrs: false
})
</script>

<script lang="ts" setup>
type IconProps = {
  name?: string
  size?: string | number
  color?: string
  iconStyle?: _typeObj | any
}

const props = withDefaults(defineProps<IconProps>(), {
  // icon 名称
  name: '',
  // icon 大小
  size: 32,
  // icon 颜色
  color: '#333',
  // 自定义icon样式
  iconStyle: {}
})

const wrapStyle = computed(() => {})
</script>

<template>
  <div class="mt-icon" :class="'mt-icon-' + name" :style="{ fontSize: size + 'rpx', color: color, ...iconStyle }"></div>
</template>

<style lang="scss" scoped></style>
