<template>
  <div class="app-container">
    <search :query-form-data="queryForm" @sumbitSearch="searchForm" />
    <tables :table="dataTable" @onRowClick="rowClick">
      <!--自定义当前列-->
      <template slot="username" slot-scope="props">
        <a class="template-username" style="color: blueviolet;border:1px solid #ccc" :href="'/#/bombscreen?mobile=' + props.obj.row.id" target="_blank">{{ props.obj.row.username }}</a>
      </template>
    </tables>

    <div ref="pageBox">
      <pageTotal :page-total="total" @returnPageSize="changePageSize" @returnPageList="changePageList" />
    </div>
  </div>
</template>

<script>
import search from '@/components/unitManagerComp/search'
import tables from '@/components/unitManagerComp/table'
import pageTotal from '@/components/unitManagerComp/pageTotal'
import { listPayerByPage } from '@/api/base/unitManager/payer'

export default {
  name: 'VueName',
  components: {
    search,
    tables,
    pageTotal
  },
  data () {
    return {
      queryForm: [
        {
          name: '姓名、手机号或EMAIL',
          prop: 'keyword',
          type: 'input'
        }
      ],
      // tableHeight: 0,
      total: 1,
      limit: 10,
      page: 1,
      dataTable: {
        tr: [
          {
            label: '编码',
            prop: 'payerId'
          },
          {
            label: '名称',
            prop: 'payerName'
          },
          {
            label: '电话',
            prop: 'tel'
          },
          {
            label: '邮箱',
            prop: 'email'
          },
          {
            label: '最后修改',
            prop: 'updateTime'
          }
        ],
        operation: {
          label: '操作', // 操作列的行首文字
          width: '200',
          data: [ // 操作列数据
            {
              label: '编辑', // 按钮文字
              Fun: 'commitDate', // 点击按钮后触发的父组件事件
              size: 'mini', // 按钮大小
              id: '1', // 按钮循环组件的key值
              classname: 'show', // 按钮的类名
              type: 'primary'
            }, {
              label: '删除',
              Fun: 'deleteDate',
              size: 'mini',
              id: '2',
              classname: 'show',
              type: 'danger'
            }
          ]
        },
        data: [
          {
            payerId: '111',
            payerName: '张三',
            tel: '黎明',
            email: '网购',
            updateTime: '2020-1-2'
          }
        ],
        border: true,
        // height: 'calc(100vh - 300px)',
        loading: false,
        align: 'center',
        hasOperation: true
      }
    }
  },
  created: {
    // this.getTableData()
  },
  methods: {
    async searchForm (searchParam) {
      this.queryForm = searchParam
      this.queryForm.page = this.page
      this.queryForm.limit = this.limit
      await listPayerByPage(this.queryForm).then(res => {
        const resData = res.data.items
        this.dataTable = resData
      })

      // this.total = this.dataTable.length
    },
    rowClick () {},
    changePageSize (data) {
      this.page = data
      this.page = 1
      this.searchForm(this.obj)
    },
    changePageList (data) {
      this.limit = data
      this.searchForm(this.obj)
    }

  }
}
</script>

<style scoped>

</style>
