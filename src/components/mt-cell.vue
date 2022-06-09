<script lang="ts" setup>
type CellProps = {
  /**
   * 标题
   */
  title?: string
  /**
   *
   */
  titleStyle?: _typeObj | any
}
const props = withDefaults(defineProps<CellProps>(), {})
</script>

<template>
  <div class="mt-cell">
    <div class="mb-1 mt-cell-title" v-if="title" :style="[titleStyle]">{{ title }}</div>
    <div class="mt-cell-lsit border-top">
      <slot></slot>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.mt-cell {
  &-title {
    font-size: 28rpx;
    color: rgba(var(--type-tips-color));
  }
}
</style>
