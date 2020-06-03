<template>
  <!-- 单选不联动 -->
  <div class="account_tree"
       id="tree_id">
    <Tree :data="treeData"
          empty-text="No Data"
          :render="renderFn"></Tree>
  </div>
</template>
<script>
export default {
  props: ['deptRow'],
  data () {
    return {
      treeData: [],
      id: ''
    }
  },
  mounted () {
    let obj = {
      api: 'getDeptTree',
      data: {}
    }
    this.getApi(obj, 'y', (json) => {
      this.getTreeData(this.treeData, json, '0')
    })
  },
  methods: {
    renderFn (h, { root, node, data }) {
      return h('span', {
        class: 'ive-tree-1',
        style: { background: data.id === this.id ? '#eaf4fe' : '#fff' }
      }, [
        h('span', [
          h('span', {
            on: {
              click: () => { this.selectChange(data) }
            }
          }, data.title)])
      ])
    },
    // 获取树的数据
    getTreeData (tree, data, index, parentName) {
      for (let i in data) {
        let obj = {
          id: data[i].id,
          title: data[i].name,
          approver: data[i].approver,
          approverName: data[i].approverName,
          parentId: data[i].parentId,
          level: index,
          children: []
        }
        if (index === '0') {
          obj.expand = true
        }
        if (this.deptRow.id && this.deptRow.id === data[i].id) {
          obj.expand = true
        }
        if (parentName) obj.parentName = parentName
        tree.push(obj)
        if (data[i].children && data[i].children.length) {
          this.getTreeData(tree[i].children, data[i].children, '', data[i].name)
        }
      }
    },
    selectChange (row) {
      this.id = row.id
      this.$emit('on-right', row)
    },
    // 接口调用
    getApi (data, errorNotice, callback) {
      this.$store.dispatch('fetchAllList', data).then(json => {
        callback && callback(json)
      }).catch(err => {
        if (errorNotice === 'y') {
          this.$Message.destroy()
          this.$Message.error(err.stateMsg)
        }
      })
    }
  }
}
</script>
<style lang="less" scoped>
#tree_id/deep/ .ivu-tree-arrow {
  height: 16px;
  line-height: 16px;
}
#tree_id/deep/ .ivu-tree ul li {
  margin: 0;
  line-height: 22px;
}
</style>
