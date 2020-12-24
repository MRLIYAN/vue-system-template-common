<template>
   <div class="person-contain">
      <div class="card">
         <el-card shadow="hover">
            <div class="username">
               <el-avatar :size="100" src="https://cube.elemecdn.com/0/88/03b0d39583f48206768a7534e55bcpng.png"></el-avatar>
               <p class="user">{{ $store.state.user.userInfo.userName }}</p>
               <p class="jitang">慢慢人生，淡然对待，一切也都会过去，而阳光总在风雨后。</p>
            </div>
            <div class="userinfo"> 
               <p><i class="el-icon-user"></i>admin</p>
               <p><i class="el-icon-ice-tea"></i>1997-01-01</p>
               <p><i class="el-icon-male"></i>男</p>
               <p><i class="el-icon-office-building"></i>广东省深圳市不知道什么地</p>
               <p><i class="el-icon-map-location"></i>汉东省-汉中市</p>
               <p><i class="el-icon-reading"></i>JavaScript、HTML、CSS、Vue、Node</p>
            </div>
            <hr>
            <div class="customtag">
               <el-tag
               :key="tag"
               v-for="tag in dynamicTags"
               closable
               :disable-transitions="false"
               @close="handleClose(tag)">
               {{tag}}
               </el-tag>
               <el-input
               class="input-new-tag"
               v-if="inputVisible"
               v-model="inputValue"
               ref="saveTagInput"
               size="small"
               @keyup.enter.native="handleInputConfirm"
               @blur="handleInputConfirm"
               >
               </el-input>
               <el-button v-else class="button-new-tag" size="small" @click="showInput">+ New Tag</el-button>
            </div>
      
         </el-card>
      </div> 
      <div class="tabs">
          <el-tabs value="first">
            <el-tab-pane label="基本信息" name="first">
               <div class="action">
                  <el-button type="primary" size="small" @click="addRows">新建用户</el-button>
                  <el-button type="danger"  size="small" @click="romoveAll">删除所选</el-button>
               </div>
               <el-table border :data="userInfoList.filter(data => !search || data.name.toLowerCase().includes(search.toLowerCase()))"
                style="width: 100%"
                @selection-change="handleSelectionChange"
                :default-sort = "{prop: 'id', order: 'ascending'}" max-height="631">
                  <el-table-column type="selection" width="55" align="center"></el-table-column>
                  <el-table-column prop="id" label="序号" width="80" sortable align="center"></el-table-column>
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
            </el-tab-pane>
            <el-tab-pane label="绑定账号" name="second">绑定账号</el-tab-pane>
         </el-tabs>
      </div>    
    
  
   </div>
</template>

<script>
export default {
   name:"personCenter",
   data() {
      return {
         dynamicTags: ['标签一', '标签二', '标签三'],
         inputVisible: false,
         inputValue: '',
         userInfoList:[
            {id:1,name:"liyan",role:"admin",email:"78945613@qq.com",createtime:"2020-12-20 12:22:22",state:1},
            {id:2,name:"zhoulei",role:"admin",email:"123456789@qq.com",createtime:"2020-12-20 12:22:22",state:0},
            {id:3,name:"liushuai",role:"admin",email:"456789132@qq.com",createtime:"2020-12-20 12:22:22",state:1},
            {id:4,name:"zhoulei",role:"admin",email:"123456789@qq.com",createtime:"2020-12-20 12:22:22",state:0},
            {id:5,name:"liushuai",role:"admin",email:"456789132@qq.com",createtime:"2020-12-20 12:22:22",state:1},
            {id:6,name:"zhoulei",role:"admin",email:"123456789@qq.com",createtime:"2020-12-20 12:22:22",state:0},
            {id:7,name:"liushuai",role:"admin",email:"456789132@qq.com",createtime:"2020-12-20 12:22:22",state:1},
            {id:8,name:"zhoulei",role:"admin",email:"123456789@qq.com",createtime:"2020-12-20 12:22:22",state:0},
            {id:9,name:"liushuai",role:"admin",email:"456789132@qq.com",createtime:"2020-12-20 12:22:22",state:1},
            {id:10,name:"zhoulei",role:"admin",email:"123456789@qq.com",createtime:"2020-12-20 12:22:22",state:0},

         ],
         search:''  
      }
   },
   created(){
      console.log(this.$store.state.user)
   },
   methods: {
      handleClose(tag) {
        this.dynamicTags.splice(this.dynamicTags.indexOf(tag), 1);
      },

      showInput() {
        this.inputVisible = true;
        this.$nextTick(() => {
          this.$refs.saveTagInput.$refs.input.focus();
        });
      },

      handleInputConfirm() {
        let inputValue = this.inputValue;
        if (inputValue) {
          this.dynamicTags.push(inputValue);
        }
        this.inputVisible = false;
        this.inputValue = '';
      },
      handleSelectionChange(val){
         console.log(val)
      },
      editRows(row){
         console.log(row)
      },
      addRows(){

      },
      romoveRows(id){
          this.userInfoList.some((item,i) => {
            if(item.id === id)
               this.userInfoList.splice(i,1)
          })
      },
      romoveAll(){

      }
      
   },
}
</script>

<style lang="scss" scoped>
   .person-contain{
      display: flex;
      justify-content: space-between;
      .card{
         width: 29%;
         margin: 20px;
         .username{
            .user{
               font-size: 24px;
               font-weight: bold;
               margin: 15px;
            }
         }
         .userinfo{

            text-align: left;

            p{
               margin-top: 18px;
               line-height: 20px;
               margin-left: 50px;
               font-size: 14px;   
            }
         }
      }
      hr{
         margin-top: 10px;
         margin-bottom: 10px;
      }
      .tabs{
         width: 70%;
         margin: 20px;
         .action{
            text-align: left;
            margin-bottom: 15px;
         }
      }

   }
   .el-tag + .el-tag {
      margin-left: 10px;
   }
   .button-new-tag {
      margin-left: 10px;
      height: 32px;
      line-height: 30px;
      padding-top: 0;
      padding-bottom: 0;
   }
   .input-new-tag {
      width: 90px;
      margin-left: 10px;
      vertical-align: bottom;
   }
</style>