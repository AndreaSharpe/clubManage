<script setup name="numberLog">
import {onMounted, ref} from 'vue'
let checkIf = ref('check')
let checkContent = ref('获取验证')
//手机号 验证码等接口
function clickCheck(){
    
    checkIf.value = 'checked'

    //后端返回请求是否成功标志 成功执行下列代码
    checkContent.value = '已发送'
    let times = 60;
    function countdown(){
        checkContent.value = times+'s'
        times--;
        if(times==-1){
            checkContent.value = '获取验证'
            checkIf.value = 'check'

            clearInterval(internalId)
        }
    }
    let internalId = setInterval(countdown, 1000);
    // setTimeout(10000)
    
}

const testData = {number:12345678900,check:1234}
let number = ref()
let check = ref()
function clickLogin(){
    //后端number check传值
    // if(number.value==testData.number&&check.value==testData.check){
    //     console.log(number.value)
    //     console.log(check.value)

    // }
    uni.navigateTo({url:'/pages/login/fillInformation'})

}

</script>

<template>
    <div class="body">
        <div class="rectangle"></div>
        <p class="title">注册账号</p>
        
        <div class="phoneNumber box">
            <img src="../../static/images/phone.svg" class="svg">
            <div class="erect"></div>
            <input class="content" type="text" placeholder="请输入手机号" v-model="number">
        </div>
        <div class="checkNum box">
            <img src="../../static/images/checkWord.svg" class="svg">
            <div class="erect"></div>
            <input class="content" type="text" placeholder="请输入验证码" v-model="check">
            <button :class="'checkNormal '+checkIf" @click="clickCheck"><p class="checkCon">{{ checkContent }}</p></button>
        </div>  
        <button class="login" @click="clickLogin"><p>登录</p></button>    
        <div class="circle"></div>
    </div>
</template>

<style scoped>
    .login p{
        left: 164px;
        top: 410.5px;
        width: 32px;
        height: 23px;
        line-height: 23px;
        color: rgba(255,255,255,1);
        font-size: 16px;
        text-align: left;
        font-family: PingFangSC-regular;
    }
    .login{
        position: absolute;
        width: 280px;
        height: 40px;
        border-radius: 16px;
        background-color: rgba(16,174,255,1);
        border: none;
        transform: translate(23px,352px);
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .checkNormal{
        position: absolute;
        transform: translate(160px,0);
        width: 70px;
        height: 24px;
        border-radius: 16px;
        border: none;
        margin-left: 45px;
        display: flex;
        align-items: center;
        justify-content: center;
    }
    .check{
        
        background-color: rgba(16,174,255,1);
    }
    .checked{
        background-color: rgba(147,210,243,1);

    }

    .checkCon{
        left: 263px;
        top: 356px;
        width: 40px;
        height: 12px;
        line-height: 12px;
        color: rgba(255,255,255,1);
        font-size: 10px;
        text-align: left;
        font-family: PingFangSC-regular;
    }
    .checked .checkCon{
        margin-left: 12px;
    }
    .erect{
        left: 90px;
        top: 294px;
        width: 1px;
        height: 16px;
        background-color: rgba(187,187,187,1);
        border: none;
        margin-right: 8px;
    }
    .box{
        display: flex;
        flex-direction: row;
        align-items: center;
        position: absolute;
        height: 40px;
        width: 280px;
        border: none;
        border-radius: 16px;
    }
    .title{
        left: 24px;
        top: 212px;
        width: 120px;
        height: 34px;
        line-height: 34px;
        color: rgba(16,16,16,1);
        font-size: 24px;
        text-align: left;
        font-family: PingFangSC-regular;
        position: absolute;
        transform: translate(0,-50px);
    }
    .checkNum{
        transform:translate(23px,292px);
        background-color: #efefef;
    }
    .phoneNumber{
        transform:translate(23px,232px);
        background-color: #efefef;
    }
    .svg{
        height: 20px;
        width: 20px;
        margin: 10px;
        margin-left: 16px;
        
    }
    .content{
        border: none;
        background-color: #efefef;
        outline: none;
        width: 100px;
    }
    /*上调*/
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
    /*上调*/
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
