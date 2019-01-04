<template>
  <div>
    <el-table :data="data">
      <el-table-column
        v-for="(item,i) in header"
        :key="i"
        :prop="item.prop"
        :label="item.display"
        :sortable="item.sortable"
        :formatter="formatter(item)"
        :width="item.width || 'auto'">
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
export default {
  props: [
    "data",
    "header"
  ],

  methods: {

    formatter(item) {
      let innerElement = null
      let copyElement = null
      let isCopy = item.isCopy
      let formatterFun = item.formatter
        return (row,col,value)=>{
            innerElement = formatterFun.call(this,row,col,value)

        }
    },
  }
}
</script>

<style lang="less">

</style>


