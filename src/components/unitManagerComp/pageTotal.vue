<template>
  <div class="page_total_box">
    <div class="page_size_box">
      <el-pagination
        style="margin-top:20px;float:right;margin-right:20px;"
        center
        background
        margin-top="10"
        :current-page="page"
        :page-sizes="[10, 20, 50, 100]"
        :page-size="limit"
        layout="total, sizes, prev, pager, next, jumper"
        :total="total"
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange"
      />
      <!-- <el-pagination
        style="margin-top:20px;float:right;margin-right:20px;"
        center
        background
        margin-top="10"
        layout="prev, pager, next, sizes, total, jumper"
        :page-sizes="[10,20,50,100]"
        :page-size="queryParams.limit"
        :total="queryParams.total"
        :current-page="queryParams.page"
        @current-change="handleCurrentChange"
        @size-change="handleSizeChange"
      /> -->
    </div>
  </div>
</template>

<script>
export default {
  name: '',
  components: {},
  props: {
    total: {
      type: Number,
      default: 0
    }
  },
  data () {
    return {
      page: 1,
      limit: 10
    }
  },
  computed: {},
  watch: {},
  created () {},
  mounted () {},
  methods: {
    handleSizeChange (val) {
      this.limit = val
      this.$emit('returnPageList', val)
    },
    handleCurrentChange (val) {
      this.page = val
      this.$emit('returnPageSize', val)
    }
  }
}
</script>

<style scoped>
.page_total_box{
    border-top: none;
    height: 48px;
}
.page_total_box .page_size_box{
    margin-top: 8px;
    float: right;
    margin-right: 30px
}
</style>
