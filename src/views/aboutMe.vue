// 个人介绍页面(后续改为动态的)
<template>
  <div>
    <div class="wrapper marginTop wow slideInLeft">
     <div class="block aboutMe">
       <div class="avatar">
         <!-- <img src="https://portrait.gitee.com/uploads/avatars/user/2763/8289321_huang-rijian_1614261509.png!avatar100" alt=""> -->
        <img src="../assets/img/007.jpg" alt="">
       </div>
            <p><span class="threed threeds">王文硕</span></p>
            <p><span class="threed threeds">男、00后</span></p>
            <p><span class="threed threeds">大二学生、现居天津市</span></p>
            <p><span class="threed threeds">一名编程学习者，为投奔IT行业而努力</span></p>
            <p><span class="threed threeds">是万千预备程序猿中的一只</span></p>
            <p><span class="threed threeds">喜欢编程，喜欢探索新技术，热爱运动，大学生活迷茫过，失落过，还好没有放弃</span></p>
            <p><span class="threed threeds">希望看到这里的你也不要轻易地放弃</span></p>
            <p><span class="threed threeds">这条路上的你并不是孤军奋战，有千千万万的猿在陪你前行</span></p>
            <p><span class="threed threeds">联系方式：wws__qln@163.com</span></p>
            <p>
            <span class="threed threeds"><a href="http://localhost:8081/wikq.xyz#/detail/169">个人简历</a></span>
            </p>
            <!-- <div class="bottom">
              本博客已经开源，源码上传到gitee。本博客前端采用vue+element-ui+axios、MVVM架构模式，后端采用nodejs+express+mysql。如果有不清楚的欢迎来信。
            </div> -->
     </div>
    </div>
  </div>
</template>

<script>
import WOW from 'wowjs';
  export default {
    name:'aboutMe',
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
  .aboutMe {
    background-color: rgba(0, 0, 0,0);
    color: #fff;
    margin-bottom: 350px;
    .avatar {
      display: flex;
      justify-content: center;
      img {
        border-radius: 50%;
        width: 100px;
      }
    }
    
    p {
      font-size: 15px;
      text-align: center;
      span {
        line-height: 45px
      }
    }
    .bottom {
      margin-top: 20px;
      padding: 20px;
      background-color: rgb(222, 223, 224);
      color: rgb(107, 106, 106);
      border-radius: 5px;
      line-height: 30px;
    }
  }
  .threed {
    font-size: 18px!important;
  }
</style>