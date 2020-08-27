<template>
  <div id="search">
    <el-form
      ref="queryForm"
      :model="queryForm"
      :inline="true"
      size="small"
      style="margin-top:10px;"
      class="demo-form-inline"
    >
      <el-form-item
        v-for="item in queryFormData"
        :key="item.label"
        :label="item.label"
        :prop="item.prop"
      >
        <el-input
          v-if="item.type == 'input'"
          v-model="queryForm[item.prop]"
          :placeholder="'请输入' + item.name"
          clearable
        />

        <el-select
          v-if="item.type == 'select'"
          v-model="queryForm[item.prop]"
          :placeholder="'请选择' + item.name"
        >
          <el-option
            v-for="option in item.options"
            :key="option.value"
            :label="option.label"
            :value="option.value"
          />
        </el-select>

        <el-date-picker
          v-if="item.type == 'time'"
          v-model="queryForm[item.prop]"
          class="timeInput"
          type="date"
          :placeholder="'请选择' + item.name"
          value-format="yyyy-MM-dd"
        />
      </el-form-item>

      <el-form-item style="margin-left:20px">
        <el-button type="primary" icon="el-icon-search" @click="handleQuery">搜索</el-button>
        <el-button icon="el-icon-refresh" @click="resetQuery">重置</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>

export default {
  name: 'Search',
  // 在子组件内部，使用props选项声明获取的数据，即接收来自父组件中的数据
  props: {
    queryFormData: {
      type: Array,
      default () {
        return []
      }
    }
  },
  data () {
    return {
      queryForm: {}
    }
  },
  computed: {},
  created () {
    this.queryFormData.forEach(item => {
      this.$set(this.queryForm, item.prop, '')
    })
  },
  methods: {
    handleQuery () {
      const searchParam = { ...this.queryForm }
      this.$emit('sumbitSearch', searchParam)
    },
    resetQuery () {
      this.$refs['searchForm'].resetFields()
    }
  }
}
</script>

<style scoped>
#search {
    background: white;
    padding: 20px 0 2px;
    border: 1px solid #ebeef5;
    margin-bottom: 20px;
}
</style>
