<template>
    <div class="group" @click="clickGroup">
        <div class="photo"><img herf="#"></div>
        <div class="contents">
            <div class="middle">
                <div class="groupName">{{ list.name }}</div>
                <div class="time">{{ list.time }}</div>
            </div>
            <div class="tail">
                <div class="LastMessage">最新一条信息</div>
                <div class="messageNum"><p class="num">2</p></div>
            </div>
        </div>
    </div>
</template>

<script setup>
    let list = {name:'哇哈哈事业部',time:'17:42'}
    function clickGroup(){
        //跳转路由
        uni.navigateTo({url:'/pages/main/chat'})

    }
</script>

<style scoped>

    .contents{
        display: flex;
        flex-direction: column;
        width: 280px;
    }
    .photo{
        margin-left: 10px;
        margin-right: 10px;

        height: 50px;
        width: 50px;
        border-radius: 50%;
        background-color: blueviolet;
    }
    .group{
        margin: 8px;
        margin-bottom: 10px;
        width: 322px;
        height: 51px;
        display: flex;
        flex-direction: row;
        background-color: rgb(255, 255, 255);

    }
    .middle{
        height: 50px;
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: space-between;
    }
    .time{
        font-size: 12px;
    }
    .groupName{
        font-size: 14px;
        height: 15px;
    }
    .tail{
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: space-between;

    }
    .LastMessage{
        font-size: 10px;
    }

    .messageNum{
        border-radius: 50%;
        height: 20px;
        width: 20px;
        background-color: rgba(255,22,0,1);
        margin: 2px;
        display: flex;
        align-items: center;
        justify-content: center;
        

    }
    .messageNum .num{
        font-size: 10px;
        color: aliceblue;
    }
</style>