<script lang="ts">
defineComponent({
  name: 'MtImage',
  inheritAttrs: false
})
</script>

<script lang="ts" setup>
type ImageProps = {
  /**
   * 图片地址 必传
   */
  src: string
  /**
   * 裁剪模式 与 uni-app 的 image 组件的 mode 参数完全一致
   */
  mode?: string
  /**
   * 宽度, 单位任意, 如果为数值, 则为rpx单位
   */
  width?: string | number
  /**
   * 高度, 单位任意, 如果为数值, 则为rpx单位
   */
  height?: string | number
  /**
   * 图片形状, circle - 圆形, square - 方形
   */
  shape?: string
  /**
   * 圆角值, 单位任意, 如果为数值, 则为rpx单位
   */
  borderRadius?: string | number
  /**
   * 是否懒加载, 仅微信小程序、App、百度小程序、字节跳动小程序有效
   */
  lazyLoad?: boolean
  /**
   * 是否开启长按图片显示识别小程序码菜单, 仅微信小程序有效
   */
  showMenuByLongpress?: boolean
  /**
   * 是否显示加载中的图标或者自定义的slot
   */
  showLoading?: boolean
  /**
   * 是否显示加载错误的图标或者自定义的slot
   */
  showError?: boolean
  /**
   * 是否需要淡入效果
   */
  fade?: boolean
  /**
   * 过渡时间, 单位ms
   */
  duration?: string | number
  /**
   * 背景颜色, 用于深色页面加载图片时, 为了和背景色融合
   */
  bgColor?: string
}

const props = withDefaults(defineProps<ImageProps>(), {
  // 图片地址
  src: '',
  // 裁剪模式 与 uni-app 的 image 组件的 mode 参数完全一致
  mode: 'aspectFill',
  // 宽度, 单位任意, 如果为数值, 则为rpx单位
  width: '100%',
  // 高度, 单位任意, 如果为数值, 则为rpx单位
  height: '100%',
  /**
   * 图片形状, circle - 圆形, square - 方形
   */
  shape: 'square',
  // 圆角值, 单位任意, 如果为数值, 则为rpx单位
  borderRadius: 0,
  // 是否懒加载, 仅微信小程序、App、百度小程序、字节跳动小程序有效
  lazyLoad: true,
  // 是否开启长按图片显示识别小程序码菜单, 仅微信小程序有效
  showMenuByLongpress: true,
  // 是否显示加载中的图标或者自定义的slot
  showLoading: true,
  // 是否显示加载错误的图标或者自定义的slot
  showError: true,
  // 是否需要淡入效果
  fade: true,
  // 过渡时间, 单位ms
  duration: 500,
  // 背景颜色, 用于深色页面加载图片时, 为了和背景色融合
  bgColor: '#f3f4f5'
})

/**
 * 组件数据
 */
const imageData = ref({
  // 图片是否加载错误, 如果是, 则显示错误占位图
  isError: false,
  // 初始化组件时, 默认为加载中状态
  loading: true,
  // 不透明度, 为了实现淡入淡出的效果
  opacity: 1,
  // 过渡时间, 因为props的值无法修改, 故需要一个中间值
  durationTime: props.duration as number,
  // 图片加载完成时, 去掉背景颜色, 因为如果是png图片, 就会显示灰色的背景
  backgroundStyle: {}
})

watch(
  () => props.src,
  (src) => {
    if (!src) {
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
  // 通过调用addUnit()方法, 如果有单位, 如百分比, px单位等, 直接返回, 如果是纯粹的数值, 则加上rpx单位
  style.width = addUnit(props.width)
  style.height = addUnit(props.height)
  // 如果是配置了圆形, 设置50%的圆角, 否则按照默认的配置值
  style.borderRadius = props.shape == 'circle' ? '50%' : addUnit(props.borderRadius)
  // 如果设置圆角, 必须要有hidden, 否则可能圆角无效
  style.overflow = props.borderRadius > 0 ? 'hidden' : 'visible'

  return style
})

/**
 * 图片加载失败
 */
const HandlerOnError = (err: Event) => {
  imageData.value.loading = false
  imageData.value.isError = true
}

/**
 * 图片加载完成, 标记loading结束
 */
const HandlerOnLoad = () => {
  imageData.value.loading = false
  imageData.value.isError = false

  // 如果不需要动画效果, 就不执行下方代码, 同时移除加载时的背景颜色
  // 否则无需fade效果时, png图片依然能看到下方的背景色
  if (!props.fade) return removeBgColor()
  // 原来opacity为1(不透明, 是为了显示占位图), 改成0(透明, 意味着该元素显示的是背景颜色, 默认的灰色), 再改成1, 是为了获得过渡效果
  imageData.value.opacity = 0
  // 这里设置为0, 是为了图片展示到背景全透明这个过程时间为0, 延时之后延时之后重新设置为duration, 是为了获得背景透明(灰色)
  // 到图片展示的过程中的淡入效果
  imageData.value.durationTime = 0
  // 延时50ms, 否则在浏览器H5, 过渡效果无效
  setTimeout(() => {
    imageData.value.durationTime = props.duration as number
    imageData.value.opacity = 1
    setTimeout(() => {
      removeBgColor()
    }, imageData.value.durationTime)
  }, 50)
}

/**
 * 移除图片的背景色
 */
const removeBgColor = () => {
  // 淡入动画过渡完成后, 将背景设置为透明色, 否则png图片会看到灰色的背景
  imageData.value.backgroundStyle = {
    backgroundColor: 'transparent'
  }
}

/**
 * 计算属性
 */
const calcAddUnit = (field: any) => {
  return addUnit(field)
}
</script>

<template>
  <div class="mt-image" :style="[wrapStyle, imageData.backgroundStyle]">
    <image
      v-if="!imageData.isError"
      :src="src"
      :mode="mode"
      @error="HandlerOnError"
      @load="HandlerOnLoad"
      :lazy-load="lazyLoad"
      class="mt-image__image"
      :style="{
        borderRadius: shape == 'circle' ? '50%' : calcAddUnit(props.borderRadius)
      }"
    ></image>
    <view
      v-if="showLoading && imageData.loading"
      class="mt-image__loading"
      :style="{
        borderRadius: shape == 'circle' ? '50%' : calcAddUnit(props.borderRadius),
        backgroundColor: bgColor
      }"
    >
      <slot v-if="$slots.loading" name="loading" />
      <mt-icon v-else name="loading1" size="40" is-rotate color="#000"></mt-icon>
    </view>

    <view
      v-if="showError && imageData.isError && !imageData.loading"
      class="mt-image__error"
      :style="{
        borderRadius: shape == 'circle' ? '50%' : calcAddUnit(borderRadius),
        backgroundColor: bgColor
      }"
    >
      <slot v-if="$slots.error" name="error" />
      <mt-icon v-else name="jinggao" size="40" color="#000"></mt-icon>
    </view>
  </div>
</template>

<style lang="scss" scoped>
.mt-image {
  position: relative;
  transition: opacity 0.5s ease-in-out;

  &__image {
    width: 100%;
    height: 100%;
  }

  &__loading,
  &__error {
    position: absolute;
    top: 0;
    left: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100%;
    height: 100%;
  }
}
</style>
