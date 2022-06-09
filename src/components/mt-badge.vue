<script lang="ts" setup>
type BadgeProp = {
  /**
   * 标记数量
   */
  value?: string | number
  /**
   * 标记显示类型
   * 'default' | 'success' | 'error' | 'warning' | 'info'
   */
  type?: string
  /**
   * 标记的颜色
   */
  color?: string
  /**
   * 标记受控显示
   */
  show?: boolean
  /**
   * 标记为 0 时是否显示
   */
  showZero?: boolean
  /**
   * 标记显示进度
   */
  processing?: boolean
  /**
   * 标记最大数来处理溢出情况
   */
  max?: number
  /**
   * 标记是否显示为点
   */
  dot?: boolean
}
const props = withDefaults(defineProps<BadgeProp>(), {
  value: undefined,
  type: 'default',
  color: undefined,
  show: true,
  showZero: true,
  processing: false,
  max: 99,
  dot: false
})

/**
 * 根据最大数 (max) 来处理溢出情况
 */
const calcValueMax = computed(() => {
  let { value, max } = props
  if (value > max) {
    return `${max}+`
  } else {
    return value
  }
})
</script>

<template>
  <div
    class="mt-badge"
    :class="[
      'mt-badge-' + type,
      {
        'mt-badge--dot': dot,
        'mt-badge--as-is': !$slots.default
      }
    ]"
  >
    <slot></slot>
    <div
      class="mt-badge-sup"
      v-if="showZero ? show : false"
      :style="{
        color: color
      }"
    >
      <div v-if="!dot">{{ calcValueMax }}</div>
      <div v-if="processing" class="mt-base-wave" :class="['mt-base-wave-' + type]"></div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.mt-badge {
  display: inline-flex;
  position: relative;
  vertical-align: middle;

  .mt-badge-sup {
    position: absolute;
    bottom: calc(100% - 18rpx);
    left: 100%;
    z-index: 1;

    display: flex;
    align-items: center;
    height: 36rpx;
    padding: 0 12rpx;
    border-radius: 18rpx;

    font-size: 24rpx;
    font-variant-numeric: tabular-nums;
    line-height: 36rpx;
    text-align: center;
    color: rgb(var(--white));

    background: rgb(var(--type-error-dark));
    transition: background-color 0.3s cubic-bezier(0.4, 0, 0.2, 1), color 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    transform: translateX(-50%);
  }

  &-default {
    .mt-badge-sup {
      background: rgb(var(--type-error-dark));
    }
  }
  &-success {
    .mt-badge-sup {
      background: rgb(var(--type-success-dark));
    }
  }
  &-error {
    .mt-badge-sup {
      background: rgb(var(--type-error-dark));
    }
  }
  &-warning {
    .mt-badge-sup {
      background: rgb(var(--type-warning-dark));
    }
  }
  &-info {
    .mt-badge-sup {
      background: rgb(var(--type-info-dark));
    }
  }

  &.mt-badge--dot {
    .mt-badge-sup {
      left: 100%;
      bottom: calc(100% - 8rpx);
      width: 16rpx;
      min-width: 16rpx;
      height: 16rpx;
      padding: 0;

      &::before {
        content: '';
        position: absolute;
        left: 0;
        right: 0;
        top: 0;
        bottom: 0;
        border-radius: 18rpx;
        transform: scale(1);
        opacity: 0;
      }
    }
  }
  &.mt-badge--as-is {
    .mt-badge-sup {
      position: static;
      transform: translateX(0);
    }
  }

  .mt-base-wave {
    position: absolute;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    border-radius: inherit;
    z-index: 1;
    animation-duration: 2s;
    animation-iteration-count: infinite;
    animation-delay: 1s;
    animation-timing-function: cubic-bezier(0, 0, 0.2, 1);
    animation-name: badge-wave-spread;

    &-default {
      color: rgb(var(--type-error-dark));
    }
    &-success {
      color: rgb(var(--type-success-dark));
    }
    &-error {
      color: rgb(var(--type-error-dark));
    }
    &-warning {
      color: rgb(var(--type-warning-dark));
    }
    &-info {
      color: rgb(var(--type-info-dark));
    }
  }
}

@keyframes badge-wave-spread {
  from {
    box-shadow: 0 0 0.5px 0px currentColor;
    opacity: 0.6;
  }
  to {
    box-shadow: 0 0 0.5px 4.5px currentColor;
    opacity: 0;
  }
}
</style>
