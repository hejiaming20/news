<!--
 * @Author: your name
 * @Date: 2020-07-23 09:57:34
 * @LastEditTime: 2020-11-12 16:59:29
 * @LastEditors: Please set LastEditors
 * @Description: 辅材仓库管理页面
 * @FilePath: \www_admin_masterd:\vue项目\BRSS-web-project\pages\warehouse\am.vue
-->
<template>
  <div>
    <div class="c_table-title"><i class="iconfont icon-biaoti1"/> 申请报废轧辊</div>
    <Table-easy
      :table-data="tableData"
      :page-size="pageSize"
      :total="total"
      :table-height="400"
      class="layout-default-margin"
      @color-table="color_table"
      @handle-current-change="handleCurrentChange"
      @handle-size-change="handleSizeChange">
      <template slot="TableHead">
        <el-row>
          <el-col :span="20">
            <el-form
              ref="ruleForm"
              :model="searchInfo1"
              :inline="true"
              label-width="80px">
              <el-form-item
                label="轧辊类型"
                prop="roll_no">
                <el-select
                  v-model="searchInfo1.roll_typeid"
                  placeholder="请选择">
                  <el-option
                    v-for="item in options"
                    :key="item.key"
                    :label="item.value"
                    :value="item.key"/>
                </el-select>
              </el-form-item>
              <el-form-item
                label="机架范围"
                prop="framerangeid">
                <el-select
                  v-model="searchInfo1.framerangeid"
                  placeholder="请选择">
                  <el-option
                    v-for="item in option_fanwei"
                    :key="item.key"
                    :label="item.value"
                    :value="item.key"/>
                </el-select>
              </el-form-item>
            </el-form>
          </el-col>
          <el-col :span="4">
            <div class="btn">
              <el-button
                size="mini"
                type="primary"
                @click="findAll()">查询
              </el-button>
              <el-button
                size="mini"
                type="primary"
                @click="resetForm('ruleForm')">重置
              </el-button>
            </div>
          </el-col>
        </el-row>
      </template>
      <template slot="TableBody">
        <el-table-column
          prop="roll_no"
          label="辊号"/>
        <el-table-column
          prop="roll_type"
          label="轧辊类型"/>
        <el-table-column
          prop="factory"
          label="制造厂商"/>
        <el-table-column
          label="轧辊材质"
          prop="material"/>
        <el-table-column
          prop="frame_no"
          label="机架号"/>
        <el-table-column
          prop="loomingposition"
          label="上机位置"/>
        <el-table-column
          prop="roll_diameter"
          label="当前辊径"/>
        <el-table-column
          prop="scrap_diameter"
          label="报废直径"/>
        <el-table-column
          prop="iaccident"
          min-width="100px"
          label="事故辊标记"/>
        <el-table-column
          prop="scrapreason"
          label="报废原因"/>
        <el-table-column
          prop="operateuser"
          label="操作人员"/>
        <el-table-column
          prop="operatetime"
          label="操作时间"/>
        <el-table-column
          label="操作"
          min-width="150"
          align="center">
          <template slot-scope="scope">
            <el-button
              size="mini"
              type="primary"
              @click="handleBf(scope.row)">报废
            </el-button>
          </template>
        </el-table-column>
      </template>
    </Table-easy>

    <div class="c_table-title"><i class="iconfont icon-biaoti1"/> 已报废轧辊</div>
    <Table-easy
      :table-data="tableDatan_0"
      :page-size="pageSize1"
      :total="total_1"
      :table-height="400"
      @handle-current-change="handleCurrentChange1"
      @handle-size-change="handleSizeChange1">
      <template slot="TableHead">
        <el-row>
          <el-col :span="20">
            <el-form
              ref="ruleForm"
              :inline="true"
              :model="searchInfo2"
              label-width="80px">
              <el-form-item
                label="辊号"
                prop="roll_no">
                <el-input v-model="searchInfo2.roll_no" />
              </el-form-item>
              <el-form-item
                label="轧辊类型"
                prop="roll_no">
                <el-select
                  v-model="searchInfo2.roll_typeid"
                  placeholder="请选择">
                  <el-option
                    v-for="item in optionsS"
                    :key="item.key"
                    :label="item.value"
                    :value="item.key"/>
                </el-select>
              </el-form-item>
              <el-form-item
                label="机架范围"
                prop="framerangeid">
                <el-select
                  v-model="searchInfo2.framerangeid"
                  placeholder="请选择">
                  <el-option
                    v-for="item in option_fanwei"
                    :key="item.key"
                    :label="item.value"
                    :value="item.key"/>
                </el-select>
              </el-form-item>
            </el-form>
          </el-col>
          <el-col :span="4">
            <div class="btn">
              <el-button
                size="mini"
                type="primary"
                @click="findAll_1()">查询
              </el-button>
              <el-button
                size="mini"
                type="primary"
                @click="resetForm('ruleForm')">重置
              </el-button>
            </div>
          </el-col>
        </el-row>
      </template>
      <template slot="TableBody">
        <el-table-column
          prop="roll_no"
          label="辊号"/>
        <el-table-column
          prop="roll_type"
          label="轧辊类型"/>
        <el-table-column
          prop="factory"
          label="制造厂商"/>
        <el-table-column
          label="轧辊材质"
          width="150"
          prop="material"/>
        <el-table-column
          prop="frame_no"
          label="机架号"/>
        <el-table-column
          prop="loomingposition"
          label="上机位置"/>
        <el-table-column
          prop="roll_diameter"
          label="当前辊径"/>
        <el-table-column
          prop="scrap_diameter"
          label="报废直径"/>
        <el-table-column
          prop="iaccident"
          min-width="100px"
          label="事故辊标记"/>
        <el-table-column
          prop="scrapreason"
          label="报废原因"/>
        <el-table-column
          prop="operateuser"
          label="操作人员"/>
        <el-table-column
          prop="operatetime"
          label="操作时间"/>
        <el-table-column
          prop="confirmationperson"
          label="确认人员"/>
        <el-table-column
          prop="confirmationtime"
          label="确认时间"/>
        <el-table-column
          label="操作"
          min-width="150"
          align="center">
          <template slot-scope="scope">
            <el-button
              size="mini"
              type="primary"
              @click="handleBf2(scope.row)">取消报废
            </el-button>
          </template>
        </el-table-column>
      </template>
    </Table-easy>

  </div>
</template>

<script>
import TableEasy from '@/components/TasilyTableEasy'
import { rollInformation, kucunlist, rolltypelist } from '@/api/pinClipBoard' //查询接口
import { get, post } from '@/lib/Util'

export default {
  components: {
    TableEasy
  },
  data() {
    return {
      pageIndex: 1,
      pageSize: 10,
      pageIndex1: 1,
      pageSize1: 10,
      formLabelAlign: {},
      searchInfo1: {
        roll_state: -1
      },
      searchInfo2: {
        roll_state: 6
      },
      tableData: [],
      tableDatan_0: [],
      tableDatan: [],
      options: [],
      optionsS: [], //第二个表
      option_fanwei: [],
      dialogVisible: false,
      checkAll: false,
      columnsArray: [],
      cities: [],
      isIndeterminate: true,
      total: 0,
      total_1: 0
    }
  },
  mounted() {
    this.findAll()
    this.findAll_1()
    this.findOption()
    post('/dictionary/findMapV1', { dicno: 'framefw' }).then(res => {
      this.option_fanwei = res.data //机架范围
    })
  },
  methods: {
    findAll() {
      console.log(this.searchInfo1.roll_state)
      post(rollInformation, {
        pageIndex: this.pageIndex,
        pageSize: this.pageSize,
        condition: this.searchInfo1
      }).then(res => {
        this.tableData = res.data
        this.total = res.count
        /* for (const item of res.data) {
          if (item.roll_state === 0) {
            this.tableDatan_0.push(item)
          } else {
            this.tableDatan.push(item)
          }
        }*/
      })
    },
    findAll_1() {
      console.log(this.searchInfo2.roll_state)
      post(rollInformation, {
        pageIndex: this.pageIndex1,
        pageSize: this.pageSize1,
        condition: this.searchInfo2
      }).then(res => {
        this.tableDatan_0 = res.data
        this.total_1 = res.count
      })
    },
    //第1个表某行报废，放到第二个表格
    handleBf(data) {
      this.$confirm('要报废该行, 是否继续?', '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
      })
        .then(() => {
          // console.log(data)
          data.roll_state = 0
          post('rollInformation/update', { rollInformation: data }).then(
            res => {
              if (res) {
                this.$message({
                  type: 'success',
                  message: '报废成功!'
                })
                this.findAll()
                this.findAll_1()
              }
            }
          )
          // this.findAll1()
        })
        .catch(() => {
          this.$message({
            type: 'info',
            message: '已取消报废'
          })
        })
    },
    //第二个表的某行取消报废，放到第一个表格
    handleBf2(data) {
      this.$confirm('该行报废将要移除, 是否继续?', '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
      })
        .then(() => {
          data.roll_state = -1
          post('rollInformation/update', { rollInformation: data }).then(
            res => {
              if (res) {
                this.$message({
                  type: 'success',
                  message: '报废成功!'
                })
                this.findAll()
                this.findAll_1()
              }
            }
          )
          // this.findAll()
        })
        .catch(() => {
          this.$message({
            type: 'info',
            message: '已取消移除报废'
          })
        })
    },
    //轧辊类型-下拉框数据
    findOption() {
      post(rolltypelist, {
        dicno: 'rolltype'
      }).then(res => {
        this.options = res.data
        this.optionsS = res.data //第二个表
      })
    },
    resetForm(formName) {
      this.$refs[formName].resetFields()
    },
    //颜色变化
    color_table(row) {
      console.log('单元格变色', row)
      if (row.row.roll_no === 'GDC09272' && row.columnIndex === 0) {
        return {
          background: 'red'
        }
      }
    },
    //分页之对应页
    handleCurrentChange(val) {
      this.pageIndex = val
      this.findAll()
    },
    //分页之一页多少条
    handleSizeChange(val) {
      this.pageSize = val
      this.findAll()
    },
    //分页之对应页
    handleCurrentChange1(val) {
      this.pageIndex1 = val
      this.findAll_1()
    },
    //分页之一页多少条
    handleSizeChange1(val) {
      this.pageSize1 = val
      this.findAll_1()
    },
    openDialoy(val) {
      console.log(val)
      this.dialogVisible = true
    },

    handleCheckAllChange(val) {
      this.checkedCities = val ? this.cities : []
      this.isIndeterminate = false
    },
    handleCheckedCitiesChange(value) {
      console.log('val', value)
    }
  }
}
</script>

<style>
.column-search {
  margin-left: 20px;
}
</style>
