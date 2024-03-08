<script setup>
    import {ref} from 'vue'
    import Select from '../../compoments/select.vue'
    
    let options = [{value:'戏剧社',label:'戏剧社'},{value:'推理社',label:'推理社'},{value:'文学社',label:'文学社'},{value:'话剧社',label:'话剧社'}]
    let name = ref()
    let sex = ref()
    let studentNum = ref()
    let club = ref()

    let childref = ref()
    
   

    //数据传入后端并进行验证，成功后跳转页面
    function clickComplete(){
        uni.navigateTo({url:'/pages/main'})     

    }

    function searchHide(){
            childref.value.searchShow(false)
          }
        // childref.value.searchShow = false
    
</script>




<template>
    <div class="total" @click="searchHide">
        <div class="rectangle"></div>
        <p class="title">完善个人信息</p>
        <button class="finish" @click="clickComplete"><p>完成</p></button> 

        <div class="body" >
            <div class="bodyTop">
                <div class="div div1">
                    <div class="contents">姓名</div>
                    <div class="erect"></div>
                    <input class="contents" type="text" placeholder="请填写真实姓名">
                </div>
                <div class="div div2">
                    <div class="contents">性别</div>
                    <div class="erect"></div>
                    <input class="contents" type="text" placeholder="请填写真实性别">
                </div>
            </div>
            <div class="div div3">
                <div class="contents">学号</div>
                <div class="erect"></div>
                <input class="contents studentNum" type="text" placeholder="请输入学号">
            </div>
            <div class="div div4">
                <div class="contents">社团</div>
                <div class="erect"></div>
                    <!-- <input class="contents studentNum" type="text" placeholder="请输入社团名称"> -->
                
                    <!-- <el-select v-model="club" placeholder="请输入社团名称" class="select" filterable multiple :reserve-keyword="false" :popper-append-to-body="false">
                    <el-option v-for="items in options" :key="items.value" :label="items.label" :value="items.value" ></el-option>
                    </el-select> -->
            </div>
            
        </div>
         
        <div class="circle"></div>
    </div>
    <Select ref="childref" class="Select"/>
</template>

<style scoped>
    
    .total{
        height: 100vh;
        overflow-y: hidden;
    }
    .title{
        left: 28px;
        top: 183px;
        width: 144px;
        height: 34px;
        line-height: 34px;
        color: rgba(16,16,16,1);
        font-size: 24px;
        text-align: left;
        font-family: PingFangSC-regular;
        transform: translate(20px,140px);

    }

    .finish p{
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
    .finish{
        position: absolute;
        width: 292px;
        height: 40px;
        border-radius: 16px;
        background-color: rgba(16,174,255,1);
        border: none;
        transform: translate(46px,380px);
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .body{
        position: absolute;
        transform: translate(40px,190px);
    }

    .bodyTop{
        display: flex;
        flex-direction: row;
    }
    .div{
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-self: center;
        border-radius: 16px;
        background-color: rgba(239,239,239,1);
        font-size: 12px;
        margin: 10px;
        margin-left: 6px;
    }

    .div1{
        width: 152px;
        height: 40px;
        
    }
    .div2{
        width: 133px;
        height: 40px;
    }
    .div3{
        width: 292px;
        height: 40px;
    }

    .div4{
        width: 292px;
        height: 40px;
        padding-bottom: 5px;
    }

    .contents{
        color: rgba(108,108,108,1);
        font-size: 10px;
        text-align: left;
        font-family: PingFangSC-regular;
        border: none;
        outline: none;
        background-color: #efefef;
        margin: 5px;
    }

    .contents:nth-child(1){
        font-weight: bold;
        margin-right: 8px;
        margin-left: 8px;

    }

    .contents:nth-child(3){
        width: 70px;
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
        width: 293px;
        height: 287px;
        background-color: rgba(255,255,255,1);
        border: 50px solid rgb(163, 224, 255);
        border-radius: 100%;
        transform: translate(-200px,520px);


    }   
    .Select{
        position: absolute;
        transform: translate(91px,-400px);
    }
    
    
    
</style>
