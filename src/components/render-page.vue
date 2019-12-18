<template>
  <div class="widget-list">
    <template v-for="item in list">
      <div
        v-if="item.type === 'formList'"
        class="widget-form-list"
        :style="$util.formatStyle(item.style)"
        :key="item.key"
      >
        <template v-for="formItem in item.list">
          <WidgetItems ref="wgList" :item="formItem" :key="formItem.key" />
        </template>
      </div>
      <WidgetItems v-else ref="wgList" :item="item" :key="item.key"/>{{item.cmdInfo}}
    </template>
  </div>
</template>

<script>
import WidgetItems from "@/components/widget-items";
import { valiDate, submit } from "@/assets/js/validate"
export default {
  name: "renderPage",
  components: {
    WidgetItems
  },
  props: {
    list: Array
  },
  data() {
    return {
      formData: {},
      showCode: false,
    };
  },
  methods: {
      //async
      handleSubmit() {
      // let res = await axios.post('/deviceControl',{
      //   serial_num: '111',
      //   productId: '0000',
      //   operation: '23232',
      //   controlParams: '32323',
      //   account: '123123'
      // })
      // let c = this.getAttribute('data-cmd_name')
      // console.log(res.data)
      console.log(event.target)
    },
    valiAllDate(list) {
      for (const item of list) {
        if (item.type === "formList") {
          let res = this.valiAllDate(item.list);
          if (res !== true) return res;
        }
        if (!item.apiKey) continue;
        let res = valiDate(item);
        if (res === true) {
          this.formatParam(item);
          continue
        }
        return res;
      }
      return true;
    },
    formatParam(item) {
      if (!item.hasOwnProperty("apiKey")) return;
      if (item.type === 'phone' && item.showCode) {
        this.formData[item.codeKey] = item.codeValue;
      }
      this.formData[item.apiKey] = item.value;
    },
    busEvent() {
      this.BUS.$on('handleClick', data => {
        switch (data.type) {
          case 'submit':
            this.handleSubmit()
            break;
          default:
            break;
        }
      });
    }
  },
  created() {
    this.busEvent()
  }
}
</script>
<style lang="stylus" scoped>
@import '~@/assets/css/widget.styl';
</style>