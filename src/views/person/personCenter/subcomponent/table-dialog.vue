<template>
    <div>
        <el-dialog :title="title+'用户信息'" :visible.sync="dialogFormVisible" width="30%" >
        <el-form :model="currentRows">
        <el-form-item label="用户名" label-width="90px">
            <el-input v-model="currentRows.name" autocomplete="off"></el-input>
        </el-form-item> 
        <el-form-item label="密码" label-width="90px">
            <el-input v-model="currentRows.name" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="邮箱" label-width="90px">
            <el-input v-model="currentRows.email" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="角色权限" label-width="90px">
            <el-input v-model="currentRows.role" autocomplete="off"></el-input>
        </el-form-item>
        </el-form>
        <div slot="footer" class="dialog-footer">
        <el-button  @click="dialogFormVisible = false">取 消</el-button>
        <el-button type="primary"  @click="isOk">确 定</el-button>
        </div>
      </el-dialog>
    </div>
</template>

<script>
export default {
    name: 'table-dialog',
    data() {
        return {
            dialogFormVisible:false
        };
    },
    created() {
    },
    props:["currentRows","title"],
    mounted() {
        
    },
    methods: {
        isOk(){
            this.dialogFormVisible = false
            if(this.title === '新建'){
                this.$emit('push', this.currentRows);
            }
        }
    },
};
</script>

<style lang="scss" scoped>

</style>