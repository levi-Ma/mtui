<script lang="ts">
defineComponent({
  name: 'MtIcon',
  inheritAttrs: false
})
</script>

<script lang="ts" setup>
type IconProps = {
  /**
   * icon 名称
   */
  name?: string
  /**
   * icon 大小
   */
  size?: string | number
  /**
   * icon 颜色
   */
  color?: string
  /**
   * 自定义 icon 样式
   */
  iconStyle?: _typeObj | any
  /**
   * 是否开启 icon 旋转
   */
  isRotate?: boolean
}

const props = withDefaults(defineProps<IconProps>(), {
  // icon 名称
  name: '',
  // icon 大小
  size: 32,
  // icon 颜色
  color: '#333',
  // 自定义icon样式
  iconStyle: {},
  // 是否开启 icon 旋转
  isRotate: false
})
</script>

<template>
  <div
    class="mt-icon"
    :class="[`mt-icon-${name}`, { rotate: isRotate }]"
    :style="{ fontSize: size + 'rpx', color: color, ...iconStyle }"
  ></div>
</template>

<style lang="scss" scoped>
.mt-icon {
  display: inline-block;
  &.rotate {
    animation: RotateIcon 2s linear infinite;
  }
}

@keyframes RotateIcon {
  from {
    transform: rotate(0deg);
  }

  to {
    transform: rotate(360deg);
  }
}
</style>
