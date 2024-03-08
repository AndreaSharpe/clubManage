<script setup name="Login">
    function toNumber(){
        uni.navigateTo({url:'/pages/login/numberLog'})
    }

    function toWechat(){
        uni.navigateTo({url:'/pages/login/fillInformation'})

    }
</script>

<template> 
    <div>
        <div class="rectangle"></div>
        <p class="title">欢迎使用！</p>
        <button class="wechat box" @click="toWechat">
            <img src="../../static/images/wechat.svg" class="svg">
           
            <span class="content">授权微信登录</span>
        
        </button>
        <button class="phoneNumber box" @click="toNumber">
            <img src="../../static/images/phone.svg" class="svg">
           
            <span class="content">手机号注册登录</span>
          
        </button>
        <div class="circle"></div>
    </div>
</template>

<style scoped>
    .box{
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: center;
        position: absolute;
        height: 40px;
        width: 250px;
        border: none;
        border-radius: 10px;
    }
    .title{
        position: absolute;
        transform: translate(0,20px);
        left: 24px;
        top: 212px;
        width: 120px;
        height: 34px;
        color: rgba(16,16,16,1);
        font-size: 24px;
        text-align: left;
        font-family: PingFangSC-regular;
        
    }
    .wechat{
        transform:translate(55px,282px);
        background-color: #79e6b6;
    }
    .phoneNumber{
        transform:translate(55px,342px);
        background-color: #ECECEC;
    }
    .svg{
        margin: 12px;
        height: 24px;
        width: 24px;
        
    }
    .comtent{
        transform: translate(0,-6px);
    }
    .rectangle{
        position: absolute;
        overflow: hidden;
        transform: translate(-130px,-160px) rotate(70deg);
        left: 207.23px;
        top: -38.12px;
        width: 307px;
        height: 186px;
        line-height: 20px;
        background-color: rgba(255,255,255,1);
        color: rgba(16,16,16,1);
        font-size: 18px;
        text-align: center;
        font-family: Roboto;
        border: 50px solid rgb(163, 224, 255);
    }
    .circle{
        left: -149px;
        top: 471px;
        width: 293px;
        height: 287px;
        background-color: rgba(255,255,255,1);
        border: 50px solid rgb(163, 224, 255);
        border-radius: 100%;
        transform: translate(-200px,520px);
    }   
</style>