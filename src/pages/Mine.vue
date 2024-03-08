<template>
    <div style="height:100vh;overflow-y: hidden;">
        <div class="rectangle"></div>
        <div class="circle"></div>
        <div class="photo"><img src="#" alt=""></div>
        <div class="name">
            <img src="../static/images/person.svg" style="width: 16px;height: 16px;margin:8px">
            <div style="max-width: 100px;">{{ imformation.name }}</div>
            <div>
                <img src="../static/images/manActive.svg" style="width: 12px;height:12px;margin:8px;"
                    :class="imformation.sex">
                <img src="../static/images/woman.svg" style="width: 8px;height:8px;margin:8px;margin-left:0;"
                    :class="imformation.sex">
                <img src="../static/images/man.svg" style="width: 8px;height:8px;margin:8px;" :class="imformation.sex">
                <img src="../static/images/womanActive.svg" style="width: 12px;height:12px;margin:8px;margin-left:0;"
                    :class="imformation.sex">
            </div>
        </div>
        <div class="studentNum">
            <img src="../static/images/studentNum.svg" style="width: 16px;height: 16px;margin:8px">
            <div>{{ imformation.studentNumber }}</div>
        </div>
        <div class="clubs">
            <img src="../static/images/team.svg" style="width: 18px;height: 18px;margin:8px">
            <p style="font-size: 10px;">我加入的社团：</p>

        </div>
        <div class="clubsContent">
            <div v-for="clubItem in imformation.club" :key="imformation.club">
                <div class="club">{{ clubItem }}</div>
            </div>
        </div>

    </div>
</template>
<style scoped>
.photo {
    width: 110px;
    height: 110px;
    border-radius: 50%;
    background-color: aqua;
    transform: translate(32px, -300px);
    position: absolute;
}

.name {
    position: absolute;
    display: flex;
    flex-direction: row;
    align-items: center;
    max-width: 172px;
    height: 25px;
    border: 1px solid rgba(187, 187, 187, 1);
    transform: translate(32px, -130px);
    border-radius: 8px;
}

.studentNum {
    position: absolute;
    display: flex;
    flex-direction: row;
    align-items: center;
    width: 172px;
    height: 25px;
    border: 1px solid rgba(187, 187, 187, 1);
    transform: translate(32px, -172px);
    border-radius: 8px;
}


.woman:nth-child(1) {
    display: none;
}

.woman:nth-child(2) {
    display: none;
}

.man:nth-child(3) {
    display: none;
}

.man:nth-child(4) {
    display: none;
}

.clubs {
    display: flex;
    flex-direction: row;
    align-items: center;
    position: absolute;
    transform: translate(32px, -90px);
}

.club {
    width: 129px;
    height: 30px;
    background-color: rgba(255, 255, 255, 1);
    border: 1px solid rgba(187, 187, 187, 1);
    font-size: 15px;
    display: flex;
    align-items: center;
    padding-left: 5px;
    margin: 5px;
    border-radius: 8px;

}

.clubsContent {
    width: 300px;
    position: absolute;
    transform: translate(27px, -60px);
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;


}

.rectangle {
    position: absolute;
    overflow: hidden;
    transform: translate(-130px, -170px) rotate(70deg);
    left: 207.23px;
    top: -38.12px;
    width: 307px;
    height: 186px;
    line-height: 20px;
    background-color: rgba(255, 255, 255, 1);
    color: rgba(16, 16, 16, 1);
    font-size: 18px;
    text-align: center;
    font-family: Roboto;
    border: 50px solid rgb(163, 224, 255);
}

.circle {
    width: 293px;
    height: 287px;
    background-color: rgba(255, 255, 255, 1);
    border: 50px solid rgb(163, 224, 255);
    border-radius: 100%;
    transform: translate(-200px, 460px);
    overflow: hidden;

}
</style>

<script setup>
import { ref } from 'vue'
let imformation = { name: '张三', sex: 'man', studentNumber: "1234567890", club: ["戏剧社", "文学社", "推理社"] }
</script>