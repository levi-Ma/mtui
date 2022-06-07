<script lang="ts">
defineComponent({
  name: 'MtImage',
  inheritAttrs: false
})
</script>

<script lang="ts" setup>
type ImageProps = {
  src?: string
  mode?: string
  width?: string | number
  height?: string | number
  shape?: string
  borderRadius?: string | number
  lazyLoad?: boolean
  showMenuByLongpress?: boolean
  showLoading?: boolean
  fade?: boolean
  duration?: string | number
  bgColor?: string
}

const props = withDefaults(defineProps<ImageProps>(), {
  // 图片地址
  src: '',
  // 裁剪模式 与 uni-app 的 image 组件的 mode 参数完全一致
  mode: 'aspectFill',
  // 宽度，单位任意，如果为数值，则为rpx单位
  width: '100%',
  // 高度，单位任意，如果为数值，则为rpx单位
  height: 'auth',
  // 图片形状，circle-圆形，square-方形
  shape: 'square',
  // 圆角值，单位任意，如果为数值，则为rpx单位
  borderRadius: 0,
  // 是否懒加载，仅微信小程序、App、百度小程序、字节跳动小程序有效
  lazyLoad: true,
  // 是否开启长按图片显示识别小程序码菜单，仅微信小程序有效
  showMenuByLongpress: true,
  // 是否显示加载中的图标或者自定义的slot
  showLoading: true,
  // 是否需要淡入效果
  fade: true,
  // 过渡时间，单位ms
  duration: 500,
  // 背景颜色，用于深色页面加载图片时，为了和背景色融合
  bgColor: '#f3f4f5'
})

const imageData = ref({
  // 图片是否加载错误，如果是，则显示错误占位图
  isError: false,
  // 初始化组件时，默认为加载中状态
  loading: true,
  // 不透明度，为了实现淡入淡出的效果
  opacity: 1,
  // 过渡时间，因为props的值无法修改，故需要一个中间值
  durationTime: props.duration,
  // 图片加载完成时，去掉背景颜色，因为如果是png图片，就会显示灰色的背景
  backgroundStyle: {}
})

watch(
  () => props.src,
  (url) => {
    if (!url) {
      imageData.value.isError = true
      imageData.value.loading = false
    } else {
      imageData.value.isError = false
    }
  }
)

/**
 * 计算样式
 */
const wrapStyle = computed(() => {
  let style = {} as any
  // 通过调用addUnit()方法，如果有单位，如百分比，px单位等，直接返回，如果是纯粹的数值，则加上rpx单位
  style.width = addUnit(props.width)
  style.height = addUnit(props.height)
  // 如果是配置了圆形，设置50%的圆角，否则按照默认的配置值
  style.borderRadius = props.shape == 'circle' ? '50%' : addUnit(props.borderRadius)
  // 如果设置圆角，必须要有hidden，否则可能圆角无效
  style.overflow = props.borderRadius > 0 ? 'hidden' : 'visible'
  return style
})

/**
 * 图片加载失败
 */
const HandlerOnError = (err: Event) => {}

/**
 * 图片加载完成，标记loading结束
 */
const HandlerOnLoad = () => {}
</script>

<template>
  <div class="mt-image">
    <image
      :src="src"
      :mode="mode"
      @error="HandlerOnError"
      @load="HandlerOnLoad"
      :lazy-load="lazyLoad"
      class="mt-image__image"
    ></image>
  </div>
</template>

<style lang="scss" scoped></style>
