<template>
  <EldataTable v-bind="$data">
    <template slot="search">
      <el-form-item label="组件名称">
        <el-input v-model="form.user" placeholder="请输入"></el-input>
      </el-form-item>
      <el-form-item label="分类">
        <el-select v-model="form.categories" placeholder="请选择">
          <el-option label="前端" value="前端"></el-option>
          <el-option label="后端" value="后端"></el-option>
        </el-select>
      </el-form-item>
      <el-form-item label="状态">
        <el-select v-model="form.status" placeholder="请选择">
          <el-option label="上架" value="上架"></el-option>
          <el-option label="下架" value="下架"></el-option>
        </el-select>
      </el-form-item>
      <!-- <el-form-item><el-button type="success" size="small" >查看</el-button>
                <el-button  size="small">编辑</el-button></el-form-item> -->
    </template>
    <template>
      <el-table-column label="状态" min-width="160px">
        <template slot-scope="scope">
          <el-link v-if="scope.row.status === 'forbidden'">下架</el-link>
          <el-link type="success" v-else>上架</el-link>
        </template>
      </el-table-column>
      <el-table-column label="操作" min-width="240px">
        <template slot-scope="scope">
          <el-button type="success" size="small">查看</el-button>
          <el-button size="small">编辑</el-button>
          <el-button size="small">下架</el-button>
        </template>
      </el-table-column>
    </template>
  </EldataTable>
</template>

<script>
import EldataTable from 'el-data-table'
import {formatDate} from '../const/filter'
export default {
  components: {
    EldataTable
  },

  data() {
    return {
      form: {
        user: '',
        categories: '',
        status: false
      },
      rate: 0,
      url:
        'https://easy-mock.com/mock/5b586c9dfce1393a862d034d/example/img?a=2',
      columns: [
        {type: 'selection'},
        {prop: 'code', label: '品牌编号'},
        {prop: 'name', label: '品牌名称'},
        {prop: 'alias', label: '品牌别名'},
        {
          prop: 'status',
          label: '状态',
          formatter: row => (row.status === 'normal' ? '启用' : '禁用')
        },
        {
          prop: 'updatedAt',
          label: '时间',
          minWidth: '140px',
          formatter: row => formatDate(row.updatedAt, 'YYYY-MM-DD')
        }
      ],
      // columns: [
      //   {type: 'selection'},
      //   {prop: 'name', label: '分类名称', minWidth: '140px'},
      //   {prop: 'description', label: '分类说明', minWidth: '140px'},
      //   // {prop: 'icon', label: '图标', minWidth: '140px',}
      //   {prop: 'updateDate', label: '时间', minWidth: '140px',
      //   formatter: row => formatDate(row.updateDate,'YYYY-MM-DD')}

      // ],
      // searchForm: [
      //   {
      //     $type: 'input',
      //     $id: 'name',
      //     label: '品牌名称',
      //     width: '200px',
      //     $el: {placeholder: '1分钟只能调用10次'},
      //     rules: [{required: true, trigger: 'blur', len: 3}]
      //   }
      // ],

      form: [
        {
          $type: 'input',
          $id: 'code',
          label: '品牌编号',
          rules: [{required: true, message: '请输入分类名称', trigger: 'blur'}]
        },
        {
          $type: 'input',
          $id: 'alias',
          label: '品牌别名',
          rules: [{required: true, message: '请输入名称说明', trigger: 'blur'}]
        }
      ],
      hasPagination: true,
      hasOperation: false
    }

    // -----
  }
}
</script>

<style></style>
