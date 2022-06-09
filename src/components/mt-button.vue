<script lang="ts">
defineComponent({
  name: 'MtButton',
  inheritAttrs: false
})
</script>
<script lang="ts" setup>
type ButtonProps = {
  /**
   * 是否细边框
   */
  hairLine?: boolean
  /**
   * 按钮的预置样式: default, primary, error, warning, success
   */
  type?: string
  /**
   * 按钮尺寸: default, medium, mini
   */
  size?: string
  /**
   * 按钮形状: rectangle (矩形) circle (两边为半圆), square (带圆角)
   */
  shape?: string
  /**
   * 按钮是否镂空
   */
  plain?: boolean
  /**
   * 是否禁止状态
   */
  disabled?: boolean
  /**
   * 是否加载中
   */
  isLoading?: boolean
  /**
   * 开放能力，具体请看uniapp稳定关于button组件部分说明
   * https://uniapp.dcloud.io/component/button
   */
  openType?: string
  /**
   * 用于 <form> 组件: 点击分别会触发 <form> 组件的 submit/reset 事件
   * 取值为 submit (提交表单), reset (重置表单)
   * 未实装
   */
  formType?: string
  /**
   * 打开 APP 时, 向 APP 传递的参数, open-type=launchApp时有效
   * 微信小程序 | QQ小程序有效
   */
  appParameter?: string
  /**
   * 指定是否阻止本节点的祖先节点出现点击态, 微信小程序有效
   */
  hoverStopPropagation?: boolean
  /**
   * 指定返回用户信息的语言, zh_CN 简体中文, zh_TW 繁体中文, en 英文. 只微信小程序有效
   */
  lang?: string
  /**
   * 会话来源: open-type="contact"时有效. 只微信小程序有效
   */
  sessionFrom?: string
  /**
   * 会话内消息卡片标题. open-type="contact" 时有效
   * 默认当前标题，只微信小程序有效
   */
  sendMessageTitle?: string
  /**
   * 会话内消息卡片点击跳转小程序路径. open-type="contact" 时有效
   * 默认当前分享路径, 只微信小程序有效
   */
  sendMessagePath?: string
  /**
   * 会话内消息卡片图片. open-type="contact" 时有效
   * 默认当前页面截图，只微信小程序有效
   */
  sendMessageImg?: string
  /**
   * 是否显示会话内消息卡片.
   * 设置此参数为 true, 用户进入客服会话会在右下角显示 "可能要发送的小程序" 提示
   * 用户点击后可以快速发送小程序消息, open-type="contact" 时有效
   */
  showMessageCard?: boolean
  /**
   * 手指按下(触摸)按钮时按钮时的背景颜色
   */
  hoverBgColor?: string
  /**
   * 自定义样式，对象形式
   */
  customStyle?: _typeObj | any
  /**
   * 节流，一定时间内只能触发一次
   */
  throttleTime?: string | number
  /**
   * 按住后多久出现点击态，单位毫秒
   */
  hoverStartTime?: string | number
  /**
   * 手指松开后点击态保留时间，单位毫秒
   */
  hoverStayTime?: string | number
}

const props = withDefaults(defineProps<ButtonProps>(), {
  hairLine: true,
  type: 'default',
  size: 'default',
  shape: 'rectangle',
  plain: false,
  disabled: false,
  isLoading: false,
  openType: '',
  formType: '',
  appParameter: '',
  hoverStopPropagation: false,
  lang: 'en',
  sessionFrom: '',
  sendMessageTitle: '',
  sendMessagePath: '',
  sendMessageImg: '',
  showMessageCard: false,
  hoverBgColor: '',
  customStyle: {},
  throttleTime: 500,
  hoverStartTime: 20,
  hoverStayTime: 150
})

/**
 * 当没有传 bgColor 变量时, 按钮按下去的颜色类名
 */
const getHoverClass = computed(() => {
  let hoverClass = ''
  hoverClass = props.plain ? 'mt-' + props.type + '-plain-hover' : 'mt-' + props.type + '-hover'
  return hoverClass
})
/**
 * 在'primary', 'success', 'error', 'warning'类型下
 * 不显示边框, 否则会造成四角有毛刺现象
 */
const showHairLineBorder = computed(() => {
  if (['primary', 'success', 'error', 'warning'].indexOf(props.type) >= 0 && !props.plain) {
    return ''
  } else {
    return 'mt-hairline-border'
  }
})
/**
 * 计算按钮形状
 */
const calcShape = computed(() => {
  // rectangle (矩形) circle (两边为半圆), square (带圆角)
  if (props.type === 'text') {
    return ''
  }
  return `mt-shape-${props.shape}`
})

const emit = defineEmits(['click', 'getphonenumber', 'getuserinfo', 'error', 'opensetting', 'launchapp'])

/**
 * 按钮点击
 */
const click = (e: Event) => {
  // 进行节流控制, 每 throttle 毫秒内, 只在开始处执行
  throttle(
    () => {
      emit('click', e)
    },
    Number(props.throttleTime),
    true
  )
}

/**
 * 下面为对接 uniapp 官方按钮开放能力事件回调的对接
 */

const getphonenumber = (res: any) => {
  emit('getphonenumber', res)
}

const getuserinfo = (res: any) => {
  emit('getuserinfo', res)
}

const error = (res: any) => {
  emit('error', res)
}

const opensetting = (res: any) => {
  emit('opensetting', res)
}

const launchapp = (res: any) => {
  emit('launchapp', res)
}
</script>

<template>
  <button
    id="mt-button"
    class="mt-btn"
    :class="[
      'mt-size-' + size,
      plain ? 'mt-btn--' + type + '--plain' : '',
      isLoading ? 'mt-loading' : '',
      type !== 'text' ? (hairLine ? showHairLineBorder : 'mt-btn--bold-border') : '',
      'mt-btn--' + type,
      disabled ? `mt-btn--${type}--disabled` : '',
      calcShape
    ]"
    :hover-start-time="Number(hoverStartTime)"
    :hover-stay-time="Number(hoverStayTime)"
    :disabled="disabled"
    :form-type="formType"
    :open-type="openType"
    :app-parameter="appParameter"
    :hover-stop-propagation="hoverStopPropagation"
    :send-message-title="sendMessageTitle"
    :send-message-path="sendMessagePath"
    :lang="lang"
    :session-from="sessionFrom"
    :send-message-img="sendMessageImg"
    :show-message-card="showMessageCard"
    @getphonenumber="getphonenumber"
    @getuserinfo="getuserinfo"
    @error="error"
    @opensetting="opensetting"
    @launchapp="launchapp"
    :style="[customStyle]"
    @tap.stop="click($event)"
    :hover-class="getHoverClass"
    :loading="isLoading"
  >
    <slot></slot>
  </button>
</template>

<style lang="scss" scoped>
@import '@/style/components/button.scss';
</style>
