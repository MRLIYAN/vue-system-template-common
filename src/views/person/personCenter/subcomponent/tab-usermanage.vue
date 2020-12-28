<template>
  <div class="tab-usermanage">
    <div class="action">
        <el-button type="primary" size="small" @click="addRows">新建用户</el-button>
        <el-button type="danger"  size="small" @click="romoveAll">删除所选</el-button>
    </div>
    <el-table border :data="userInfoList.filter(data => !search || data.name.toLowerCase().includes(search.toLowerCase()))"
    style="width: 100%"
    @selection-change="handleSelectionChange"
    :default-sort = "{prop: 'id', order: 'ascending'}" max-height="631">
        <el-table-column type="selection" width="55" align="center"></el-table-column>
        <el-table-column type="index" label="序号" width="80" sortable align="center"></el-table-column>
        <el-table-column prop="name" label="姓名" width="180" align="center"></el-table-column>
        <el-table-column prop="role" label="角色" width="180" align="center"></el-table-column>
        <el-table-column prop="email" label="邮箱" align="center"></el-table-column>
        <el-table-column prop="createtime" label="创建时间" sortable align="center"></el-table-column>
        <el-table-column prop="state" label="状态" width="80" align="center"> 
            <template slot-scope="scope">
            <el-tag
                :type="scope.row.state ? 'success' : 'danger'"
                disable-transitions>{{scope.row.state ? "正常" : "异常"}}</el-tag>
            </template>
        </el-table-column>
        <el-table-column align="center">
            <template slot="header">
            <el-input
                v-model="search"
                size="mini"
                placeholder="输入关键字搜索"/>
            </template>
            <template slot-scope="scope">
            <el-button @click="editRows(scope.row)" type="text" size="small">编辑</el-button>
            <el-button type="text" size="small" @click="romoveRows(scope.row.id)">移除</el-button>
            </template>
        </el-table-column>
    </el-table>

      <!-- 编辑表格对话框 -->
     <table-dialog v-show="isShowDialog" title="编辑" :currentRows="currentRows" ref="editdialog"></table-dialog>

     <!-- 新建用户对话框 -->
     <table-dialog v-show="isShowDialog" title="新建" :currentRows="currentRows" @push="dialogPushRows" ref="editdialog"></table-dialog>
  </div>
</template>

<script>
import TableDialog from './table-dialog.vue';
import { dateFormat } from '@/utils/common'
export default {
  name: 'tab-usermanager',
  data() {
    return {
        isShowDialog:false, 
        search:'' ,
        currentRows:{},
        selectRows:[]
    };
  },
  props:["userInfoList"],
  mounted() {
    
  },
  methods: {
     handleSelectionChange(val){  //多选框改变触发函数
        this.selectRows = val
      },
      editRows(row){
        this.isShowDialog = true
        this.$refs.editdialog.dialogFormVisible = true,
        this.currentRows = row

      },
      addRows(){
        this.isShowDialog = true
        this.$refs.editdialog.dialogFormVisible = true,
        this.currentRows = {
          id:this.userInfoList.length,
          name:"",
          role:"",
          email:"",
          createtime:dateFormat("yyyy-MM-dd hh:mm:ss",new Date),
          state:1
        }
      },
      dialogPushRows(item){
        this.userInfoList.push(item)
      },
      romoveRows(id){
        this.userInfoList.some((item,i) => {
          if(item.id === id)
              this.userInfoList.splice(i,1)
            //  return true
        })
      },
      romoveAll(){
        this.selectRows.forEach(item => {
          this.userInfoList.forEach((element,i )=> {
            if(item.id === element.id)
               this.userInfoList.splice(i,1)
          })
            
          })
      },
  },
  components:{
    TableDialog
  }
};
</script>

<style lang="scss" scoped>

  .tab-usermanage{
    .action{
      text-align: left;
      margin-bottom: 15px;
    }
  }
</style>