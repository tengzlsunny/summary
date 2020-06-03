<template>
  <div class="month-range-class">
    <Poptip placement="bottom-start" v-model="visible" @on-popper-show="popperShowEvent">
      <Input v-model="monthStart" prefix="ios-calendar-outline" readonly placeholder="选择月份" style="width: 210px;margin-bottom:0px" />
      <div class="monthPanpel" slot="content">
        <div class="monthPanpel-left">
          <div class="monthPanpel-left_title">
            <span>
              <Icon type="ios-arrow-dropleft" size="20" @click="handleYearBefore('left')" style="cursor:pointer" />
            </span>
            <div>{{`${yearStart}年`}}</div>
            <!-- <span v-if="showRightBtn">
              <Icon type="ios-arrow-dropright" size="20" @click="handleYearBefore('right')" style="cursor:pointer" />
            </span> -->
          </div>
          <div class="monthPanpel-month-left_list">
            <div v-for="(item,index) in monthListLeft" :class="['monthPanpel-left-cell', item.label ? 'monthPanpel-hover-cell' : '' ]" :key="item.value"
              @click="handleMonthLeftClick('left',index, item)"
              :style="{background:(currentBgLeft[0] === index || currentBgRight[0] === index) ?'#2d8cf0':'',color:(currentBgLeft[0] === index || currentBgRight[0] === index) ?'#FFF':''}">
              <span>{{item.label}}</span>
            </div>
          </div>
        </div>
        <div class="monthPanpel-right">
          <div class="monthPanpel-right_title">
            <div>{{`${yearEnd}年`}}</div>
            <span v-show="showRightBtn">
              <Icon type="ios-arrow-dropright" size="20" @click="handleYearBefore('right')" style="cursor:pointer" />
            </span>
          </div>
          <div class="monthPanpel-month-right_list">
            <div v-for="(item,index) in monthListRight" :class="['monthPanpel-right-cell', item.label ? 'monthPanpel-hover-cell' : '']" :key="item.value"
              @click="handleMonthLeftClick('right',index, item)"
              :style="{background:(currentBgLeft[1] === index || currentBgRight[1] === index) && item.label ?'#2d8cf0':'',color:(currentBgLeft[1] === index || currentBgRight[1] === index) && item.label?'#FFF':''}">
              <span>{{item.label}}</span>
            </div>
          </div>
        </div>
      </div>
    </Poptip>
  </div>
</template>
<script>
export default {
  props: {
    /**
     * initData: 初始化值
     */
    initData: { type: String }
  },
  watch: {
    initData: {
      handler (val) {
        this.monthStart = this.initData
      },
      immediate: true
    }
  },
  data () {
    return {
      visible: false,
      clickNum: 0,
      yearStart: new Date().getFullYear() - 1,
      yearEnd: new Date().getFullYear(),
      monthStart: '',
      startT: [],
      monthListLeft: [
        { label: '1月', value: '1' },
        { label: '2月', value: '2' },
        { label: '3月', value: '3' },
        { label: '4月', value: '4' },
        { label: '5月', value: '5' },
        { label: '6月', value: '6' },
        { label: '7月', value: '7' },
        { label: '8月', value: '8' },
        { label: '9月', value: '9' },
        { label: '10月', value: '10' },
        { label: '11月', value: '11' },
        { label: '12月', value: '12' }
      ],
      monthListRight: [],
      showRightBtn: true
    }
  },
  computed: {
    currentBgLeft () {
      let index = ['', '']
      let start = ''
      if (this.startT && this.startT.length) {
        start = this.startT[0]
      } else if (this.monthStart && this.monthStart.length && this.monthStart.indexOf('~') !== -1) {
        start = this.monthStart.split('~')[0]
      }
      if (start && this.yearStart === Number(start.substring(0, 4))) {
        index[0] = this.getIndexNum(start)
      } else if (start && this.yearEnd === Number(start.substring(0, 4))) {
        index[1] = this.getIndexNum(start)
      }
      return index
    },
    currentBgRight () {
      let index = ['', '']
      let end = ''
      if (this.startT && this.startT.length === 1) {
        end = ''
      } else if (this.monthStart && this.monthStart.length && this.monthStart.indexOf('~') !== -1) {
        end = this.monthStart.split('~')[1]
      }
      if (end && this.yearStart === Number(end.substring(0, 4))) {
        index[0] = this.getIndexNum(end)
      } else if (end && this.yearEnd === Number(end.substring(0, 4))) {
        index[1] = this.getIndexNum(end)
      }
      return index
    }
  },
  mounted () {
    this.getRightMonth()
  },
  methods: {
    // 获取当前右侧月份
    getRightMonth () {
      let date = new Date()
      let year = date.getFullYear()
      let month = date.getMonth()
      this.monthListRight = JSON.parse(JSON.stringify(this.monthListLeft))
      if (this.yearEnd >= year) {
        for (let i in this.monthListRight) {
          let obj = { label: '', value: Number(i) + 1 + '' }
          if (i > month) this.monthListRight[i] = obj
        }
        this.showRightBtn = false
      } else {
        this.showRightBtn = true
      }
    },
    // 获取当前选中的下标值
    getIndexNum (val) {
      let index = ''
      if (val.substring(val.length - 2, val.length - 1) === '0') {
        index = Number(val.substring(val.length - 1, val.length)) - 1
      } else {
        index = Number(val.substring(val.length - 2, val.length)) - 1
      }
      return index
    },
    popperShowEvent () {
      this.startT = []
    },
    handleMonthLeftClick (type, index, item) {
      if (!item.label) return
      if (type === 'left' && this.startT.length < 2) {
        let mon = (index + 1 + '').padStart(2, 0)
        let startT = `${this.yearStart}-${mon}`
        this.startT.push(startT)
      } else if ((type = 'right' && this.startT.length < 2)) {
        let mon = (index + 1 + '').padStart(2, 0)
        let startT = `${this.yearEnd}-${mon}`
        this.startT.push(startT)
      }
      if (this.startT.length >= 2) {
        // eslint-disable-next-line no-unused-expressions
        new Date(this.startT[0]).getTime() >
          new Date(this.startT[1]).getTime()
          ? this.startT.reverse()
          : ''
        this.monthStart = this.startT.join('~')
        this.visible = false
        this.$emit('on-month-range', this.monthStart)
      }
    },
    handleYearBefore (type) {
      if (type === 'left') {
        this.yearStart -= 2
        this.yearEnd -= 2
      } else if (type === 'right') {
        this.yearEnd += 2
        this.yearStart += 2
      }
      this.getRightMonth()
    }
  }
}
</script>
<style lang="less" scoped>
.month-range-class {
  display: flex;
  align-items: center;
  .monthPanpel {
    display: flex;
    .monthPanpel-left,
    .monthPanpel-right {
      width: 180px;
      display: flex;
      flex: 1;
      flex-wrap: wrap;
      .monthPanpel-left_title,
      .monthPanpel-right_title {
        width: 100%;
        padding: 10px;
        font-size: 12px;
        display: flex;
        align-items: center;
        border-bottom: 1px solid #e8eaec;
        > div {
          text-align: center;
          width: 100%;
          font-size: 12px;
          height: 20px;
          line-height: 20px;
        }
      }
      .monthPanpel-month-left_list,
      .monthPanpel-month-right_list {
        display: flex;
        flex-wrap: wrap;
        align-items: center;
        justify-content: space-between;
      }
      .monthPanpel-month-left_list {
        margin-right: 12px;
      }
      .monthPanpel-month-right_list {
        margin-left: 12px;
      }
      .monthPanpel-left-cell,
      .monthPanpel-right-cell {
        width: 36px;
        text-align: center;
        height: 26px;
        line-height: 26px;
        margin: 6px 10px;
        border-radius: 3px;
      }
      .monthPanpel-hover-cell:hover {
        cursor: pointer;
        background: #e1f0fe;
      }
    }
  }
}
</style>
<style lang="less">
.month-range-class {
  .ivu-poptip-body {
    padding: 0;
  }
}

.month-range-class .ivu-input {
  padding-left: 10px;
}
.month-range-class .ivu-input-prefix {
  right: 0;
  left: auto;
}
</style>
