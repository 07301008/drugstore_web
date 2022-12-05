<template>
  <div>
    <div style="margin-bottom: 5px;">
      <el-input v-model="name" placeholder="姓名" suffix-icon="el-icon-search" style="width: 200px;"
                @keyup.enter.native="getPage"
      ></el-input>
      <el-select v-model="sex" style="margin-left: 5px;" filterable placeholder="请选择性别">
        <el-option
            v-for="item in sexs"
            :key="item.value"
            :label="item.label"
            :value="item.value">
        </el-option>
      </el-select>
      <el-button type="primary" style="margin-left: 5px;" @click="getPage">查询</el-button>
      <el-button type="success" @click="resetParam">重置</el-button>
    </div>
    <el-table :data="tableData"
              :header-cell-style="{background:'#f3f6fd', color: '#555'}"
    >
      <el-table-column prop="id" label="ID" width="60" align="center">
      </el-table-column>
      <el-table-column prop="username" label="用户名" width="120" align="center">
      </el-table-column>
      <el-table-column prop="name" label="姓名" width="120" align="center">
      </el-table-column>
      <el-table-column prop="idNumber" label="身份证号" width="200" align="center">
      </el-table-column>
      <el-table-column prop="sex" label="性别" width="60" align="center">
        <template slot-scope="scope">
          <el-tag
              :type="scope.row.sex === '1' ? 'primary' : 'success'"
              disable-transitions>{{ scope.row.sex === '1' ? '男' : '女' }}
          </el-tag>
        </template>
      </el-table-column>
      <el-table-column prop="role" label="角色" width="60" align="center">
        <template slot-scope="scope">
          <el-tag
              :type="scope.row.role === 0 ? 'danger' : (scope.row.role === 1 ? 'primary' : 'success')"
              disable-transitions>{{ scope.row.role === 0 ? '管理员' : (scope.row.role === 1 ? '店长' : '店员') }}
          </el-tag>
        </template>
      </el-table-column>
      <el-table-column prop="phone" label="手机号" width="120" align="center">
      </el-table-column>
      <el-table-column prop="createTime" label="创建时间" align="center" width="200">
      </el-table-column>
      <el-table-column prop="updateTime" label="修改时间" align="center" width="200">
      </el-table-column>
      <el-table-column prop="createUser" label="创建人" width="80" align="center">
      </el-table-column>
      <el-table-column prop="updateUser" label="修改人" width="80" align="center">
      </el-table-column>
      <el-table-column prop="status" label="状态" width="60" align="center">
        <template slot-scope="scope">
          <el-tag
              :type="scope.row.status === 1 ? 'primary' : 'danger'"
              disable-transitions>{{ scope.row.status === 1 ? '启用' : '禁用' }}
          </el-tag>
        </template>
      </el-table-column>
      <el-table-column prop="operate" label="操作" width="200" align="center">
        <el-button size="small" type="primary">编辑</el-button>
        <el-button size="small" type="danger">删除</el-button>
      </el-table-column>
  </el-table>
    <!--分页工具条-->
    <el-pagination
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange"
        :current-page="currentPage"
        :page-sizes="[5, 10, 15, 20]"
        :page-size="pageSize"
        layout="total, sizes, prev, pager, next, jumper"
        :total="totalCount">
    </el-pagination>
  </div>
</template>
<script>
export default {
  name: "Main",
  data() {
    return {
      // 每页展示条数
      pageSize:5,
      // 总记录数
      totalCount:100,
      // 当前页码
      currentPage: 1,
      // 表数据
      tableData: [],
      // 输入的姓名
      name: '',
      // 性别
      sex: '',
      sexs: [
          {
            value: '1',
            label: '男'
          }, {
            value: '0',
            label: '女'
          }
      ]
    }
  },
  methods:{
    getPage(){
      this.$axios.get(this.$httpUrl+'/employee/page?currentPage='+this.currentPage+
          "&pageSize="+this.pageSize+"&name="+this.name+"&sex="+this.sex)
          .then(res=>res.data).then(res=>{
        console.log(res)
        if (res.code == 1){
          this.tableData = res.data.rows
          this.totalCount = res.data.totalCount
        }else {
          alert(res.msg);
        }

      })
    },
    resetParam(){
      this.name = '';
      this.sex = '';
    },
    loadPost(){
      this.$axios.post(this.$httpUrl+'/employee',{}).then(res=>res.data).then(res=>{
        console.log(res)
      })
    },
    // 每页显示条数发生变化后执行
    handleSizeChange(val) {
      this.pageSize = val;
      this.getPage();
    },
    // 当前页码发生变化后执行
    handleCurrentChange(val) {
      // console.log(`当前页: ${val}`)
      // 重新设置当前页码
      this.currentPage = val;
      this.getPage();
    }
  },
  beforeMount() {
    this.getPage();
    // this.loadPost();
  }
}
</script>

<style scoped>

</style>