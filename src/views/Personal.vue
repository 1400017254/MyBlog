// 个人主页
<template>
  <div class="wrapper wow slideInLeft">
    <div class="content">
      <el-form ref="form" :rules="rules" label-width="80px" :inline="false" size="normal">
        <el-form-item label="昵称">
          <el-input v-model="nickname"></el-input>
        </el-form-item>
        <el-form-item label="头像">
          <!-- 上线后更改127.0.0.1 -->
          <el-upload
            class="avatar-uploader"
            action="http://127.0.0.1:3000/api/article/upload"
            :show-file-list="false"
            :on-success="handleAvatarSuccess"
            :before-upload="beforeAvatarUpload"
            name="head_img"
            >
            <img :src="imageUrl" class="avatar">
            <!-- <i v-else class="el-icon-plus avatar-uploader-icon"></i> -->
          </el-upload>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" @click="onSubmit">保存</el-button>
          <el-button @click="exit">退出登录</el-button>
        </el-form-item>
      </el-form>
      
    </div>
  </div>
</template>

<script>
import WOW from '../assets/js/wow';
import Cookie from 'js-cookie'
export default {
    data() {
      return {
        form:{
          nickname:''
        },
        imageUrl:'',
        nickname:''
      }
    },
     methods: {
        handleAvatarSuccess(res) {
          this.imageUrl = res.data
        },
      beforeAvatarUpload(file) {
        const isJPG = file.type === 'image/jpeg';
        const isLt2M = file.size / 1024 / 1024 < 2;

        if (!isJPG) {
          this.$message.error('上传头像图片只能是 JPG 格式!');
        }
        if (!isLt2M) {
          this.$message.error('上传头像图片大小不能超过 2MB!');
        }
        return isJPG && isLt2M;
      },
      exit(){
        // 清除Cookie
        Cookie.set('token','')
        // 清除sessionStorage
        sessionStorage.clear();
        this.$router.push({path:'/'})
        location.reload();
      },
      // 获取用户信息
      GetInfo(){
         this.$http.get('http://127.0.0.1:3000/api/users/info').then( (res) => {
          //  获取用户头像地址
           this.nickname = res.data.data.nickname
           this.imageUrl = res.data.data.head_img
         })
      },
      // 更新用户信息
      async onSubmit(){
        // if(this.nickname === '王先森' && this.imageUrl === this.imageUrl){
        //   return this.$message.error('昵称已经被占用了，请换一个昵称吧~');
        // }
        await this.$http.post('/api/users/updateUser',{
          nickname:this.nickname,
          head_img:this.imageUrl
        })
        // 刷新页面
        location.reload();
      }

    },
    created(){
      this.GetInfo();
      console.log(this.defaultAvatar);
    },
    mounted(){
      	let wow = new WOW.WOW({
          boxClass: 'wow',
          animateClass: 'animated',
          offset: 0,
          mobile: true,
          live: true
        });
        wow.init();
    }
  }
</script>

<style lang="scss" scoped>
.content {
  width: 30%;
  margin: 5% auto;
  color: #fff!important;
}

  /deep/.el-form-item__label {
      font-size: 14px;
      color: #fff!important;
  }
// 头像
  .avatar-uploader .el-upload {
    border: 1px dashed #d9d9d9;
    border-radius: 6px;
    cursor: pointer;
    position: relative;
    overflow: hidden;
  }
  /deep/.avatar-uploader-icon:hover {
    border-color: #ffffff!important;
  }
  .avatar-uploader-icon {
    font-size: 28px;
    color: #8c939d;
    width: 178px;
    height: 178px;
    line-height: 178px;
    text-align: center;
  }
  .avatar {
    width: 178px;
    height: 178px;
    display: block;
  }
</style>