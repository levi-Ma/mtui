<script lang="ts" setup>
/**
 * 所有的 icon
 */
const list = ref([
  { name: 'danxuanfill', title: '单选-fill' },
  { name: 'danxuan', title: '单选' },
  { name: 'fangxingweixuanzhong', title: '方形未选中' },
  { name: 'fangxingxuanzhongfill', title: '方形选中-fill' },
  { name: 'fangxingxuanzhong', title: '方形选中' },
  { name: 'guanbi12', title: '关闭1' },
  { name: 'guanbi2fill', title: '关闭2-fill' },
  { name: 'guanbi21', title: '关闭2' },
  { name: 'jiahao', title: '加号' },
  { name: 'jiahao1', title: '加号1' },
  { name: 'jiahao2fill', title: '加号2-fill' },
  { name: 'jianhao', title: '减号' },
  { name: 'tishifill', title: '提示-fill' },
  { name: 'tishi3', title: '提示' },
  { name: 'wenhaofill', title: '问号-fill' },
  { name: 'wenhao', title: '问号' },
  { name: 'xuanze', title: '选择' },
  { name: 'yuanxingweixuanzhong', title: '圆形未选中' },
  { name: 'yuanxingxuanzhongfill', title: '圆形选中-fill' },
  { name: 'yuanxingxuanzhong', title: '圆形选中' },
  { name: 'biaoxingfill', title: '标星-fill' },
  { name: 'biaoxing', title: '标星' },
  { name: 'chexiao', title: '撤销' },
  { name: 'dianpufill', title: '店铺-fill' },
  { name: 'dianpu', title: '店铺' },
  { name: 'dingdan', title: '订单' },
  { name: 'fankui', title: '反馈' },
  { name: 'fenxiang1', title: '分享' },
  { name: 'gengduo', title: '更多' },
  { name: 'gonglve', title: '攻略' },
  { name: 'gouwuchefill', title: '购物车-fill' },
  { name: 'gouwuche', title: '购物车' },
  { name: 'gouwudai', title: '购物袋' },
  { name: 'qiapianxingshi', title: '卡片形式' },
  { name: 'kefufill', title: '客服-fill' },
  { name: 'kefu1', title: '客服' },
  { name: 'liebiaoxingshi', title: '列表形式' },
  { name: 'liuyanfill', title: '留言-fill' },
  { name: 'liuyan', title: '留言' },
  { name: 'pengyoufill', title: '朋友-fill' },
  { name: 'pengyou', title: '朋友' },
  { name: 'qingchu', title: '清除' },
  { name: 'quan', title: '券' },
  { name: 'saoma', title: '扫码' },
  { name: 'shaixuan1', title: '筛选' },
  { name: 'shanchu', title: '删除' },
  { name: 'shezhi1', title: '设置' },
  { name: 'shenfen', title: '身份' },
  { name: 'shizhongfill', title: '时钟-fill' },
  { name: 'shizhong', title: '时钟' },
  { name: 'shouyefill', title: '首页-fill' },
  { name: 'shouye', title: '首页' },
  { name: 'sousuo2', title: '搜索' },
  { name: 'sousuoleimufill', title: '搜索类目-fill' },
  { name: 'sousuoleimu', title: '搜索类目' },
  { name: 'taobao', title: '淘宝' },
  { name: 'taojinbi', title: '淘金币' },
  { name: 'tianmao', title: '天猫' },
  { name: 'tongzhifill', title: '通知-fill' },
  { name: 'tongzhi1', title: '通知' },
  { name: 'tuikuan', title: '退款' },
  { name: 'wangwangfill', title: '旺旺-fill' },
  { name: 'wangwang', title: '旺旺' },
  { name: 'wodefill', title: '我的-fill' },
  { name: 'wode', title: '我的' },
  { name: 'wuliu', title: '物流' },
  { name: 'xihuanfill', title: '喜欢-fill' },
  { name: 'xihuan1', title: '喜欢' },
  { name: 'xinxifill', title: '信息-fill' },
  { name: 'xinxi', title: '信息' },
  { name: 'youhuiquan', title: '优惠券' },
  { name: 'yuyan', title: '语言' },
  { name: 'zhengli', title: '整理' },
  { name: 'zuji', title: '足迹' },
  { name: 'zuobiaofill', title: '坐标-fill' },
  { name: 'zuobiao', title: '坐标' },
  { name: 'dibu1', title: '底部' },
  { name: 'dingbujinzhi', title: '顶部-禁止' },
  { name: 'dingbu1', title: '顶部' },
  { name: 'xiangshang3', title: '向上3' },
  { name: 'xiangxia5', title: '向下5' },
  { name: 'xiangyou2', title: '向右2' },
  { name: 'xiangzuo2', title: '向左2' },
  { name: 'xiangji1fill', title: '相机1-fill' },
  { name: 'xiangji1', title: '相机1' },
  { name: 'xiangji2', title: '相机2' },
  { name: 'wifi1', title: 'wifi' },
  { name: 'hongbao1', title: '红包' },
  { name: 'xinyongqia', title: '信用卡' },
  { name: 'shoujitaobao', title: '手机淘宝' },
  { name: 'yonghufill', title: '用户-fill' },
  { name: 'yonghu', title: '用户' },
  { name: 'juhuasuan', title: '聚划算' },
  { name: 'salefill', title: 'sale-fill' },
  { name: 'sale', title: 'sale' },
  { name: 'zengsong', title: '赠送' },
  { name: 'androidgengduo', title: 'Android更多' },
  { name: 'leimu', title: '类目' },
  { name: 'bangzhuzhongxin', title: '帮助中心' },
  { name: 'caidan1', title: '菜单' },
  { name: 'zantongfill', title: '赞同-fill' },
  { name: 'zantong', title: '赞同' },
  { name: 'xiangshang4', title: '向上4' },
  { name: 'xiangxia4', title: '向下4' },
  { name: 'dianhua1', title: '电话' },
  { name: 'danpin', title: '单品' },
  { name: 'duozhongzhifu', title: '多种支付' },
  { name: 'erweima1', title: '二维码' },
  { name: 'guojiwuliu', title: '国际物流' },
  { name: 'huwai', title: '户外' },
  { name: 'jujia', title: '居家' },
  { name: 'kuzi', title: '裤子  ' },
  { name: 'muying', title: '母婴' },
  { name: 'nanzhuang', title: '男装' },
  { name: 'neiyi', title: '内衣' },
  { name: 'nvzhuang', title: '女装' },
  { name: 'pinpai', title: '品牌' },
  { name: 'tequanzhuanshu', title: '特权专属' },
  { name: 'xiangbao', title: '箱包' },
  { name: 'yishouchu', title: '已售出' },
  { name: 'ditu', title: '地图' },
  { name: 'dianhua', title: '电话' },
  { name: 'yanjing_guanbi', title: '眼睛_关闭' },
  { name: 'zhiding', title: '置顶' },
  { name: 'Home', title: 'Home' },
  { name: 'zhizhen', title: '指针' },
  { name: 'ID', title: 'ID' },
  { name: 'yinhangka', title: '银行卡' },
  { name: 'caidan', title: '菜单' },
  { name: 'shang', title: '上' },
  { name: 'xia', title: '下' },
  { name: 'zuo', title: '左' },
  { name: 'you', title: '右' },
  { name: 'dingbu', title: '顶部' },
  { name: 'dibu', title: '底部' },
  { name: 'shang1', title: '上' },
  { name: 'xia1', title: '下' },
  { name: 'you1', title: '右' },
  { name: 'zuo1', title: '左' },
  { name: 'zuo2', title: '左' },
  { name: 'shangxia', title: '上下' },
  { name: 'you2', title: '右' },
  { name: 'zuoyou', title: '左右' },
  { name: 'fangda', title: '放大' },
  { name: 'zhankai', title: '展开' },
  { name: 'suoxiao', title: '缩小' },
  { name: 'shouqi', title: '收起' },
  { name: 'shang2', title: '上' },
  { name: 'you3', title: '右' },
  { name: 'zuo3', title: '左' },
  { name: 'xia2', title: '下' },
  { name: 'shang3', title: '上' },
  { name: 'zuo4', title: '左' },
  { name: 'you4', title: '右' },
  { name: 'xia3', title: '下' },
  { name: 'zuo5', title: '左' },
  { name: 'you5', title: '右' },
  { name: 'xia4', title: '下' },
  { name: 'shang4', title: '上' },
  { name: 'bohao', title: '拨号' },
  { name: 'lanya', title: '蓝牙' },
  { name: 'saoyisao', title: '扫一扫' },
  { name: 'shipin', title: '视频' },
  { name: 'shouji1', title: '手机' },
  { name: 'zhendong', title: '震动' },
  { name: 'WiFi', title: 'WiFi' },
  { name: 'ios', title: 'ios' },
  { name: 'anzhuo', title: '安卓' },
  { name: 'guan', title: '关' },
  { name: 'kai', title: '开' },
  { name: 'guanbi11', title: '关闭' },
  { name: 'jianshao', title: '减少' },
  { name: 'jinggao', title: '警告' },
  { name: 'queren', title: '确认' },
  { name: 'kaishi', title: '开始' },
  { name: 'quxiao', title: '取消' },
  { name: 'zanting', title: '暂停' },
  { name: 'tianjia', title: '添加' },
  { name: 'tuichu', title: '退出' },
  { name: 'tishi1', title: '提示' },
  { name: 'zhengchang', title: '正常' },
  { name: 'dengdai', title: '等待' },
  { name: 'danxian', title: '单线' },
  { name: 'shuangxian', title: '双线' },
  { name: 'dianzhuangtu', title: '点状图' },
  { name: 'bingzhuangtu', title: '饼状图' },
  { name: 'quyutu', title: '区域图' },
  { name: 'shangchuan', title: '上传' },
  { name: 'shangsheng', title: '上升' },
  { name: 'xiajiang', title: '下降' },
  { name: 'zhuzhuangtu', title: '柱状图' },
  { name: 'zhexiantu', title: '折线图' },
  { name: 'zengchangtu', title: '增长图' },
  { name: 'xiazai', title: '下载' },
  { name: 'anquan_changyong', title: '安全_常用' },
  { name: 'anquan_sousuo', title: '安全_搜索' },
  { name: 'bianji_2', title: '编辑_2' },
  { name: 'bianji_1', title: '编辑_1' },
  { name: 'anquan_zichan', title: '安全_资产' },
  { name: 'bifen', title: '比分' },
  { name: 'biaoqian', title: '标签' },
  { name: 'biaoji', title: '标记' },
  { name: 'bianjiqi', title: '编辑器' },
  { name: 'dengji', title: '等级' },
  { name: 'cunkuan', title: '存款' },
  { name: 'biaoqing', title: '表情' },
  { name: 'dianzan', title: '点赞' },
  { name: 'fasong', title: '发送' },
  { name: 'erweima', title: '二维码' },
  { name: 'fanzhuan_you', title: '翻转_右' },
  { name: 'fanzhuan_zuo', title: '翻转_左' },
  { name: 'fenxiang', title: '分享' },
  { name: 'geren_jianshao', title: '个人_减少' },
  { name: 'fuzhi', title: '复制' },
  { name: 'geren_qiehuan', title: '个人_切换' },
  { name: 'geren_tianjia', title: '个人_添加' },
  { name: 'guanbi2', title: '关闭' },
  { name: 'jiesuo', title: '解锁' },
  { name: 'geren', title: '个人' },
  { name: 'jinggao1', title: '警告' },
  { name: 'jineshuaxin', title: '金额刷新' },
  { name: 'jiangbei', title: '奖杯' },
  { name: 'hongbao', title: '红包' },
  { name: 'lajitong', title: '垃圾桶' },
  { name: 'kefu', title: '客服' },
  { name: 'liwu', title: '礼物' },
  { name: 'paizhao', title: '拍照' },
  { name: 'lianjie', title: '链接' },
  { name: 'qianbao', title: '钱包' },
  { name: 'qiandao', title: '签到' },
  { name: 'qingli', title: '清理' },
  { name: 'quanping', title: '全屏' },
  { name: 'riqi', title: '日期' },
  { name: 'qunzu', title: '群组' },
  { name: 'qunzu_jianshao', title: '群组_减少' },
  { name: 'qunzu_tianjia', title: '群组_添加' },
  { name: 'shaixuan', title: '筛选' },
  { name: 'shengyin', title: '声音' },
  { name: 'shezhi', title: '设置' },
  { name: 'tupian', title: '图片' },
  { name: 'suoding', title: '锁定' },
  { name: 'tishi11', title: '提示' },
  { name: 'tongzhi-1', title: '通知-1' },
  { name: 'tongzhi', title: '通知' },
  { name: 'wenjian_sousuo', title: '文件_搜索' },
  { name: 'wenjian_shuaxin', title: '文件_刷新' },
  { name: 'wenjian_baohu', title: '文件_保护' },
  { name: 'wenjian_tishi', title: '文件_提示' },
  { name: 'xuanzhong', title: '选中' },
  { name: 'xiaoxi_2', title: '消息_2' },
  { name: 'xingbie_nv', title: '性别_女' },
  { name: 'xiaoxi_1', title: '消息_1' },
  { name: 'xingbie_nan', title: '性别_男' },
  { name: 'yanjing_dakai', title: '眼睛_打开' },
  { name: 'loading', title: 'loading' },
  { name: 'loading1', title: 'loading' },
  { name: 'mima', title: '密码' },
  { name: 'shouji', title: '手机' },
  { name: 'shijian', title: '时间' },
  { name: 'aixin', title: '爱心' },
  { name: 'shoucang', title: '收藏' },
  { name: 'aixin1', title: '爱心' },
  { name: 'shoucang1', title: '收藏' },
  { name: 'tishi', title: '提示' },
  { name: 'wuwangluo', title: '无网络' },
  { name: 'fujian-shangchuanchenggong', title: '附件-上传成功' },
  { name: 'shangchuanshibai', title: '上传失败' }
])

/**
 * 复制 icon 的 name 到剪切板
 */
const handelCopyIcon = (name: string) => {
  uni.setClipboardData({
    data: name
  })
}
</script>

<template>
  <div class="p-4 page-container">
    <div class="p-4 mb-8 rounded-lg module-wrap">
      <div class="title">Icon 图标</div>
      <div class="grid grid-rows-1 module-list">
        <div class="module-item">
          <div class="my-2 tit">基本用法</div>
          <mt-icon name="biaoxing"></mt-icon>
        </div>
        <div class="module-item">
          <div class="my-2 tit">旋转图标</div>
          <mt-icon name="loading1" size="50" :is-rotate="true"></mt-icon>
        </div>
        <div class="module-item">
          <div class="my-2 tit">设置icon大小</div>
          <mt-icon name="biaoxing" size="50"></mt-icon>
        </div>
        <div class="module-item">
          <div class="my-2 tit">设置icon颜色</div>
          <mt-icon name="biaoxing" size="50" color="red"></mt-icon>
        </div>
        <div class="module-item">
          <div class="my-2 tit">自定义icon样式</div>
          <div class="grid grid-cols-4 list">
            <div class="item">
              <mt-icon name="biaoxing" :icon-style="{ fontSize: '60rpx', color: 'green' }"></mt-icon>
            </div>
            <div class="item">
              <mt-icon name="biaoxing" :icon-style="{ fontSize: '20rpx', color: 'green' }"></mt-icon>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="grid grid-cols-3 items">
      <div
        class="flex flex-col flex-center py-3 rounded item"
        v-for="(item, index) in list"
        :key="index"
        @click="handelCopyIcon(item.name)"
      >
        <mt-icon :name="item.name" size="50"></mt-icon>
        <div class="tit">{{ item.title }}</div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.items {
  gap: 20rpx;

  .item {
    background: #fff;
  }
}
.tit {
  font-size: 24rpx;
  color: #000;
}
</style>
