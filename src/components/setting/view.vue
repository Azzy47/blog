<template>
    <div class="setting">
        <el-tabs type="border-card" class="el-tabs">
            <el-tab-pane>
                <span slot="label"><i class="el-icon-date"></i> 资料设置</span>
                <form action="" class="infoForm">
                    <el-form :label-position="labelPosition" label-width="80px" :model="infoForm">
                        <el-form-item label="头像">
                            <el-upload
                                class="avatar-uploader"
                                action="https://jsonplaceholder.typicode.com/posts/"
                                :show-file-list="false"
                                :on-success="handleAvatarSuccess"
                                :before-upload="beforeAvatarUpload">
                                <img v-if="imageUrl" :src="imageUrl" class="avatar">
                                <i v-else class="el-icon-plus avatar-uploader-icon"></i>
                            </el-upload>
                            <p class="tips">支持 jpg格式大小 5M 以内的图片</p>
                        </el-form-item>
                        <el-form-item label="昵称">
                            <el-input v-model="infoForm.username" clearable></el-input>
                        </el-form-item>
                        <el-form-item label="ID">
                            <el-input v-model="infoForm.ID" clearable></el-input>
                        </el-form-item>
                        <el-form-item label="性别" prop="gender">
                            <el-radio-group v-model="infoForm.resource">
                                <el-radio label="男"></el-radio>
                                <el-radio label="女"></el-radio>
                            </el-radio-group>
                        </el-form-item>
                        <el-form-item label="生日" prop="birth">
                            <div class="block">
                                <el-date-picker
                                    v-model="infoForm.birth"
                                    type="date"
                                    placeholder="选择日期">
                                </el-date-picker>
                            </div>
                        </el-form-item>
                        <el-form-item label="个性签名">
                            <el-input v-model="infoForm.ID" clearable></el-input>
                        </el-form-item>
                    </el-form>
                </form>
                 <!--  -->
            </el-tab-pane>
            <el-tab-pane label="修改密码">
                <form action="" class="passForm">
                    <el-form :label-position="labelPosition" label-width="80px" :model="infoForm">
                        <el-form-item label="旧密码" prop="passWord">
                            <el-input v-model="passForm.passWord" placeholder="请输入密码" show-password clearable autocomplete="off"></el-input>
                        </el-form-item>
                        <el-form-item label="新密码1" prop="passWord">
                            <el-input v-model="passForm.passWord" placeholder="请输入新密码" show-password clearable autocomplete="off"></el-input>
                        </el-form-item>
                        <el-form-item label="新密码2" prop="checkPass">
                            <el-input v-model="passForm.checkPass" placeholder="再次输入新密码" show-password clearable  autocomplete="off"></el-input>
                        </el-form-item>
                    </el-form>
                </form>
            </el-tab-pane>
            <el-tab-pane label="角色管理">角色管理</el-tab-pane>
            <el-tab-pane label="定时任务补偿">定时任务补偿</el-tab-pane>
        </el-tabs>

    </div>
</template>
<style scoped>
    @import "../../css/common.css";
    a{
        font-size: 20px;
    }
    .setting{
        background-color: #fafafa;
        background-position: 50% 50%;
        width: 100%;
        height: 780px;
        padding: 100px;
    }
    .infoForm {
        padding: 20px;
        width: 70%;
        margin: 0 auto;
    }
    .passForm {
        padding: 20px;
        width: 70%;
        margin: 0 auto;
    }
    .el-tabs{
        width: 680px;
        margin: 0 auto;
        background: rgba(255,255,255,.7);
        border-radius: 5px;
    }
    .tips{
        float: left;
        margin-left: 20px;
        font-size: 14px;
        color: #606266;
    }
    .avatar-uploader{
        border: 1px solid #d9d9d9;
        width: 60px;
        height: 60px;
        border-radius: 15px;
        float: left;
    }
    .avatar-uploader-icon {
        font-size: 28px;
        color: #8c939d;
        width: 60px;
        height: 60px;
        line-height: 60px;
        text-align: center;
    }
    .avatar {
        width: 60px;
        height: 60px;
        border-radius: 15px;
        display: block;
    }
    .sub-view-box[data-v-0f32526e] .setting-list .item .title{
        font-size: 1.2rem;
        color: #333;
        width: 10rem;
    }
</style>

<script>
  export default {
    data() {
      return {
        imageUrl: '',
        labelPosition: 'left',
        infoForm: {
          avatar: '',
          username: '',
          ID: '',
          gender: '',
          birth: ''
        },
        passForm: {
          passWord: '',
          checkPass: '',
        }
      };
    },
    methods: {
      handleAvatarSuccess(res, file) {
        this.imageUrl = URL.createObjectURL(file.raw);
      },
      beforeAvatarUpload(file) {
        const isJPG = file.type === 'image/jpeg';
        const isLt5M = file.size / 1024 / 1024 < 5;

        if (!isJPG) {
          this.$message.error('上传头像图片只能是 JPG 格式!');
        }
        if (!isLt5M) {
          this.$message.error('上传头像图片大小不能超过 5MB!');
        }
        return isJPG && isLt5M;
      }
    }
  }
</script>
