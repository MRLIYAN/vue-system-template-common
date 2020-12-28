<template>
    <div class="account-bind ">
        <div class="account-item">
            <i class="el-icon-phone account-item-icon"></i>
            <div class="account-item-content">
            <p>绑定手机</p>
            <p>23456456</p>
            </div>
        <el-link type="primary">主要链接</el-link>
        </div>
        <el-divider></el-divider>
        <div class="account-item">
            <i class="el-icon-phone account-item-icon"></i>
            <div class="account-item-content">
            <p>绑定手机</p>
            <p>23456456</p>
            </div>
        <el-link type="primary">主要链接</el-link>
        </div>
    </div>
</template>

<script>
export default {
    name: 'tab-accountbind',
    data() {
        return {
            
        };
    },
    mounted() {
        
    },
    methods: {
        
    },
};
</script>

<style lang="scss" scoped>
    .account-bind{
        .account-item{
            display: flex;
            .account-item-icon{
                font-size: 30px;
                color: rgb(52, 146, 237);
            }
            .account-item-content{
                flex: 1;
                text-align: left;
                margin-left: 20px;
            }

        }
    }
</style>