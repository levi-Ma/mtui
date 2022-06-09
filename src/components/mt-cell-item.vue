<script lang="ts" setup>
type CellItemProps = {
  /**
   * 用于识别被点击的是第几个cell
   */
  index?: string | number
  /**
   * 标题, 必填
   */
  title: string
  /**
   * 标题 样式
   */
  titleStyle?: _typeObj | any
  /**
   * 左侧 icon
   */
  icon?: string
  /**
   * 描述信息
   */
  label?: string
  /**
   * 是否开启点击反馈，即点击时cell背景为灰色，none为无效果
   */
  hoverClass?: string
  /**
   * 右侧内容
   */
  value?: string
  /**
   * 是否开启右侧箭头
   */
  isArrow?: boolean
  /**
   * 右侧 icon size
   */
  arrowSize?: string
  /**
   * 右侧 icon 颜色
   */
  arrowColor?: string
  /**
   * 背景颜色
   * 默认为透明背景
   */
  bgColor?: string
}
const props = withDefaults(defineProps<CellItemProps>(), {
  hoverClass: 'mt-cell-hover'
})

const emit = defineEmits(['click'])

const click = () => {
  emit('click', props.index)
}
</script>

<template>
  <view
    @click="click"
    class="flex items-center border-bottom p-2 mt-cell-item"
    :hover-class="hoverClass"
    hover-stay-time="150"
    :style="{
      backgroundColor: bgColor
    }"
  >
    <!-- 自定义左侧 icon -->
    <slot v-if="$slots.leftIcon && !icon" name="leftIcon"></slot>
    <mt-icon v-if="!$slots.leftIcon && icon" :name="icon"></mt-icon>

    <div
      class="flex flex-col mt-cell-item__left"
      :class="{
        'ml-2': $slots.leftIcon || icon
      }"
    >
      <div class="title" :style="[titleStyle]">{{ title }}</div>
      <div class="content" v-if="label">{{ label }}</div>
    </div>
    <div class="flex flex-center ml-a mt-cell-item__right">
      <div class="flex items-center mr-2">
        <!-- 自定义右侧文字 -->
        <slot v-if="$slots.rightValue && !value" name="rightValue"></slot>
        <div class="value" v-if="!$slots.rightValue && value">{{ value }}</div>
      </div>

      <!-- 自定义左侧 icon -->
      <slot v-if="$slots.rightIcon && !isArrow" name="rightIcon"></slot>
      <mt-icon v-if="!$slots.rightIcon && isArrow" name="you" :size="arrowSize" :color="arrowColor"></mt-icon>
    </div>
  </view>
</template>

<style lang="scss" scoped>
.mt-cell-item {
  .mt-cell-item__left {
    flex: 1;
  }
  .title {
    font-size: 28rpx;
  }
  .content,
  .value {
    font-size: 24rpx;
  }
  .title {
    max-width: 300rpx;
    color: rgba(var(--type-main-color));
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
  }

  .content,
  .value {
    color: rgba(var(--type-content-color));
  }
}

.mt-cell-hover {
  background-color: #f7f8f9 !important;
}
</style>
