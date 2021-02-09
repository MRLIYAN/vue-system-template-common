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
            <el-tab-pane label="用户管理" name="first">
               <tab-usermanage :userInfoList="userInfoList"></tab-usermanage>
            </el-tab-pane>
            <el-tab-pane label="绑定账号" name="second">
               <tab-accountbind></tab-accountbind>
            </el-tab-pane>
         </el-tabs>
      </div>    
    
  
   </div>
</template>

<script>
import TabAccountbind from './subcomponent/tab-accountbind.vue';
import tabUsermanage from "./subcomponent/tab-usermanage.vue"

export default{
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

      }
   },
   created(){
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
     
      
   },
   components: { tabUsermanage, TabAccountbind },
}
</script>

<style lang="scss" scoped>
   .person-contain{
      display: flex;
      justify-content: space-between;
      .card{
         width: 29%;
         .username{
            .user{
               font-size: 24px;
               font-weight: bold;
               margin: 15px;
            }
            .jitang{
               line-height: 30px;
               text-indent: 2em;
               text-align: left;
            }
         }
         .userinfo{

            text-align: left;

            p{
               margin-top: 18px;
               line-height: 20px;
               margin-left: 25px;
               font-size: 16px; 
               i{
                  margin-right: 10px;
               }  
            }
         }
      }
      hr{
         margin-top: 10px;
         margin-bottom: 10px;
      }
      .tabs{
         width: 70%;
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