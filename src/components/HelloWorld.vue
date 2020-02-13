<template>
  <div class="hello">
      <div class="page-contaniner my">
        <!-- 开屏广告 -->
        <div class="count-down" v-show="adBack">
          <span class="jump">点击跳转<b>{{n}}</b></span>
        </div>
        <!-- 主体 1-->
        <div class="login-contant">
          <h1 class="login-title">欢迎登录</h1>
          <div class="panel">
            <input type="text" class="mobile btn" placeholder="手机号码" v-model="mobile" />
            <p class="error-tip" v-show="!mobile">手机号码不能为空</p>
          </div>
          <div class="panel">
            <input type="text" class="password btn" placeholder="登录密码" v-model="password"/>
            <p class="error-tip" v-show="!password">密码不能为空</p>
          </div>
          <div class="panel">
            <button class="btn-login btn login" @click="login()">登录</button>
          </div>
          <div class="panel">
            <a href="" class="text">我要注册</a>
            <a href="" class="text">忘记密码</a>
          </div>
        </div>
      </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data () {
    return {
        adBack: true,//开屏广告,
        n:5,
        timer:null,//定时器
        mible:"",
        password:"",
    };
  },
  methods:{//方法
    //定时器
     play:function(){
      this.timer =setInterval(this.autoPlay,1000)
     },
     autoPlay:function(){
          this.n--;
          if(this.n==0){
            // this.adBack=false;//开屏隐藏
            // clearInterval(this.timer)//清除定时
            this.jump()
          }
     },
     jump:function(){
        this.adBack=false;//开屏广告隐藏
        clearInterval(this.timer)//清除定时器
     },
     //登录
     login:function(){
       //判断是否为空 加密用MD5
        if(!this.mible && !this.password){
            alert("请输入信息")
        }else{
          //发过来获取数据
            axios({
                  method:"post",//请求方式
                  url:"http://loachost:3333/from.into",//获取后台数据
                  data:JSON.stringify({
                    mobile:this.mobile,
                    password:this.password
                  }).then(function(res){//请求成功 res后端返回的结果
                      console.log(res)
                  })
            }).catch(function(error){
              console.log(error)//请求失败
            })
        }
     }
  },
  mounted:function(){//生命周期   钩子函数
    this.play()
  }
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
html,body,#app,.hello{
  width:100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  background: salmon
}
.jump{
  width: 100%;
  height: 50px;
  line-height: 50px;
  display: flex;
  justify-content: flex-start
}
.jump>b{
  margin-right: 20px;
}
</style>
