<template>
  <div class="widget-view" :key="item.key" :class="{'no-padding':noPaddingType.includes(item.type)}">
    <!-- 手机 -->
    <WgPhone v-if="item.type === 'phone'" :ref="item.key" :item="item" />

    <!-- 输入框 -->
    <WgInput v-if="item.type === 'input'" :ref="item.key" :item="item" />

    <!-- 选择框 -->
    <WgCheckbox v-if="item.type === 'checkbox'" :ref="item.key" :item="item" />

    <!-- 下拉选择 -->
    <WgSelect v-if="item.type === 'select'" :ref="item.key" :item="item" />

    <!-- 开关 -->
    <WgSwitch v-if="item.type === 'switch'" :ref="item.key" :item="item" />

    <!-- 日期选择 -->
    <WgDate v-if="item.type === 'date'" :ref="item.key" :item="item" />

    <!-- 横向滑动自动选择 -->
    <WgHorizontalPicker v-if="item.type === 'h-picker'" :ref="item.key" :item="item" />

    <!-- 图片展示 -->
    <WgImgshow v-if="item.type === 'imgShow'" :item="item" />

    <!-- 图片轮播 -->
    <wgImgSlide v-if="item.type === 'imgSlide'" :item="item" />

    <!-- 按钮 -->
    <WgButton v-if="item.type === 'button'" :item="item" />

    <!-- 文本描述 -->
    <WgStaticText v-if="item.type === 'staticText'" :item="item" />

    <!-- 分割线 -->
    <wgSplitLine v-if="item.type === 'splitLine'" :item="item" />
  </div>
</template>

<script>
import WgPhone from "./wg-phone"
import WgInput from "./wg-input"
import WgCheckbox from "./wg-checkbox"
import WgSelect from "./wg-select"
import WgSwitch from "./wg-switch"
import WgDate from "./wg-date"
import wgImgSlide from "./wg-imgslide"
import WgStaticText from "./wg-statictext"
import WgButton from "./wg-button"
import wgSplitLine from "./wg-splitLine"
import WgImgshow from "./wg-imgshow"
import WgHorizontalPicker from "./wg-horizontal-picker"
export default {
  name: "widgetItems",
  components: {
    WgPhone,
    WgInput,
    WgCheckbox,
    WgSelect,
    WgSwitch,
    WgDate,
    WgButton,
    wgSplitLine,
    WgStaticText,
    WgImgshow,
    wgImgSlide,
    WgHorizontalPicker
  },
  props: {
    item: Object,
    required: true
  },
  data() {
    return {
      noPaddingType: ['imgShow', 'staticText']
    }
  }
};
</script>
