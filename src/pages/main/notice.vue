<template>
    <div class="total">
        <div class="body">
            <div class="notice" v-for="item in notice" v-show="postContent == 'total'">
                <div class="dot" v-show="item.confirm == 0"></div>
                <div class="poster">
                    <img :src="item.poster" class="photo">
                    <p>{{ item.posterName }}</p>
                </div>
                <p style="margin-left: 15px;margin-bottom:5px;">最新公告：</p>
                <div class="listBody">
                    <div class="listLine">
                        <img src="../../static/images/time.svg" class="icon">
                        <div class="content" style="margin-right: 5px;">{{ item.month }}月{{
                            item.date }}日</div>
                        <div class="content">{{ stand(item.hour) }}:{{ stand(item.minute)
                        }}</div>
                    </div>
                    <div class="listLine">
                        <img src="../../static/images/location.svg" class="icon">
                        <div class="content">{{ item.place }}</div>

                    </div>
                    <div class="listLine" style="padding-right: 10px;">
                        <img src="../../static/images/list.svg" class="icon">
                        <div class="content" style="width:300px;">{{ item.value }}</div>
                    </div>
                    <div class="listLine">
                        <img src="../../static/images/head.svg" class="icon">
                        <div class="content" style="display:flex;flex-direction:row;justify-content:center;">
                            <p>负责人：</p>
                            <div style="display:flex;flex-direction:row;">
                                <p style="margin-right: 5px;font-size:12px;line-height: 20px;">{{ item.person.personName }}
                                </p>
                                <p style="margin-right: 5px;font-size:12px;line-height: 20px;">Tel:{{ item.person.tel }}</p>
                                <p style="margin-right: 5px;font-size:12px;line-height: 20px;">QQ:{{ item.person.QQ }}</p>
                            </div>
                        </div>
                    </div>

                </div>
                <div :class="ifConfirm(item.confirm)" @click="confirmed(item)">{{ confirm(item.confirm) }}</div>

            </div>
            <div class="notice" v-for="item in mineNotice" v-show="postContent == 'mine'">
                <div class="poster">
                    <img :src="item.poster" class="photo">
                    <p>{{ item.posterName }}</p>
                </div>
                <p style="margin-left: 15px;margin-bottom:5px;">最新公告：</p>
                <div class="listBody">
                    <div class="listLine">
                        <img src="../../static/images/time.svg" class="icon">
                        <div class="content" style="margin-right: 5px;">{{ item.month }}月{{
                            item.date }}日</div>
                        <div class="content">{{ stand(item.hour) }}:{{ stand(item.minute)
                        }}</div>
                    </div>
                    <div class="listLine">
                        <img src="../../static/images/location.svg" class="icon">
                        <div class="content">{{ item.place }}</div>

                    </div>
                    <div class="listLine" style="padding-right: 10px;">
                        <img src="../../static/images/list.svg" class="icon">
                        <div class="content" style="width:300px;">{{ item.value }}</div>
                    </div>
                    <div class="listLine">
                        <img src="../../static/images/head.svg" class="icon">
                        <div class="content" style="display:flex;flex-direction:row;justify-content:center;">
                            <p>负责人：</p>
                            <div style="display:flex;flex-direction:row;">
                                <p style="margin-right: 5px;font-size:12px;line-height: 20px;">{{ item.person.personName }}
                                </p>
                                <p style="margin-right: 5px;font-size:12px;line-height: 20px;">Tel:{{ item.person.tel }}</p>
                                <p style="margin-right: 5px;font-size:12px;line-height: 20px;">QQ:{{ item.person.QQ }}</p>
                            </div>
                        </div>
                    </div>

                </div>
                <div class="postBottom">
                    <div @click="modifyPost(item)" class="postBottomButtom">修改公告</div>
                    <div @click="deletePost(item)" class="postBottomButtom">删除公告</div>
                </div>


            </div>
            <div v-if="popShow" class="pop">
                <div class="popChild">
                    <p style="margin-left: 15px;margin-bottom:10px;">请将其添加至您的待办</p>
                    <div>
                        <div class="listLine">
                            <img src="../../static/images/time.svg" class="icon">
                            <div class="content" style="margin-right: 5px;">{{ month }}月{{
                                date }}日</div>
                            <div class="content">{{ stand(hour) }}:{{ stand(minute)
                            }}</div>
                        </div>
                        <div class="listLine">
                            <img src="../../static/images/location.svg" class="icon">
                            <div class="content">{{ place }}</div>

                        </div>
                        <div class="listLine" style="padding-right: 10px;">
                            <img src="../../static/images/list.svg" class="icon">
                            <div class="content">参加活动</div>
                        </div>
                    </div>
                    <div class="addTodo" @click="addClick">点击添加</div>
                </div>

            </div>
            <div :class="hide + showAddNotice">
                <div style="display: flex;flex-direction: row;justify-content: space-between;">
                    <p class="addNoticeTop" @click="clickPost">取消</p>
                    <p class="addNoticeTop" @click="postNotice">发布</p>
                </div>
                <div class="listBody">
                    <div class="listLine" style="margin-left: 30px;align-items:center;">
                        <img src="../static/images/time.svg" class="icon">
                        <p>时间：</p>
                        <input class="content" style="margin: 3px;background-color:white;border-radius:8px;padding:4px;"
                            placeholder="此处添加时间" v-model="time" />
                        <p style="color: grey;">ep(1.1 12:00)</p>
                    </div>
                    <div class="listLine" style="margin-left: 30px;align-items:center;">
                        <img src="../static/images/location.svg" class="icon">
                        <p>地点：</p>
                        <input class="content" placeholder="此处添加地点"
                            style="margin: 3px;background-color:white;border-radius:8px;padding:4px;" v-model="location" />

                    </div>
                    <div class="listLine" style="margin-left: 30px;">
                        <img src="../static/images/list.svg" class="icon">
                        <p>通知内容：</p>
                        <textarea class="content" placeholder="请输入具体内容  "
                            style="margin: 3px;background-color:white;border-radius:8px;padding:4px;height:120px;width:200px;"
                            v-model="event" maxlength="-1" />
                    </div>
                    <div class="listLine" style="margin-left: 30px;">
                        <img src="../../static/images/head.svg" class="icon">
                        <div class="content" style="display:flex;flex-direction:row;">
                            <p>负责人：</p>
                            <div style="display:flex;flex-direction:column;" @click="showcontents">
                                <p v-show="hideContent == 'hide'" style="color: grey;width:260px;">添加+</p>
                                <div style="display: flex;flex-direction:row;margin-bottom:6px;" v-show="hideContent == ''">
                                    <p v-show="hideContent == ''">姓名:</p>
                                    <input class="content" placeholder="请输入姓名"
                                        style="margin-left:8px;width:140px;background-color:white;border-radius:8px;padding:4px;align-items:center;"
                                        v-model="name" v-show="hideContent == ''" />
                                </div>
                                <div style="display: flex;flex-direction:row;margin-bottom:6px;" v-show="hideContent == ''">
                                    <p v-show="hideContent == ''">Tel:</p>
                                    <input class="content" placeholder="请输入手机号"
                                        style="margin-left:8px;width:140px;background-color:white;border-radius:8px;padding:4px;align-items:center;"
                                        v-model="tel" v-show="hideContent == ''" />
                                </div>
                                <div style="display: flex;flex-direction:row;margin-bottom:6px;" v-show="hideContent == ''">
                                    <p v-show="hideContent == ''">QQ:</p>
                                    <input class="content" placeholder="请输入QQ号"
                                        style="margin-left:8px;width:140px;background-color:white;border-radius:8px;padding:4px;align-items:center;"
                                        v-model="qq" v-show="hideContent == ''" />
                                </div>



                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="postNotice" @touchstart="startClickPost" @touchend="endClickPost" @click="clickPost"
                :style="`height:${height};width:${width}`"><img src="../../static/images/add.svg"
                    :style="`height: 40px;width:40px;transform:rotate(${deg}deg);`"></div>
                <div :class="`minePost ${hide}`" style="transform: translate(-92px, -572px);" @click="checkMinePost">我发布的</div>
                <div :class="`minePost ${hide}`" style="transform: translate(-92px, -540px);" @click="checkAllPost">全部公告</div>
                    
        </div>

        <div style="color:gray;margin-bottom:15px;">仅显示过去三个月的公告</div>
        <div class="title">公告</div>

    </div>
</template>


<script setup>
import { ref, watch } from 'vue'
let notice = ref([
    { poster: "../../static/images/QQ图片20231213202428.jpg", posterName: "王五", value: '1.本次活动为集体活动，要提前10分钟到达集合地，不要迟到;午饭请自带，但社团亦会准备零食等之类供给大家;另交通费及晚上聚餐费用社团承担。2.因是户外活动，请自备防晒用具;游玩时注意自身安全，尽量不要走散群队。3.请自备相机摄影留念。', month: 2, date: 5, hour: 9, minute: 0, place: '文理学部桂圆操场', person: { personName: "王五", tel: "12674634", QQ: "132434645" }, confirm: 1 },
    { poster: "../../static/images/QQ图片20231213202428.jpg", posterName: "李四", value: '1.本次活动为集体活动，要提前10分钟到达集合地，不要迟到;午饭请自带，但社团亦会准备零食等之类供给大家;另交通费及晚上聚餐费用社团承担。2.因是户外活动，请自备防晒用具;游玩时注意自身安全，尽量不要走散群队。3.请自备相机摄影留念。', month: 3, date: 3, hour: 9, minute: 0, place: '文理学部桂圆操场', person: { personName: "李四", tel: "12674634", QQ: "132434645" }, confirm: 0 },
    { poster: "../../static/images/QQ图片20231213202428.jpg", posterName: "王五", value: '1.本次活动为集体活动，要提前10分钟到达集合地，不要迟到;午饭请自带，但社团亦会准备零食等之类供给大家;另交通费及晚上聚餐费用社团承担。2.因是户外活动，请自备防晒用具;游玩时注意自身安全，尽量不要走散群队。3.请自备相机摄影留念。', month: 2, date: 7, hour: 9, minute: 0, place: '文理学部桂圆操场', person: { personName: "王五", tel: "12674634", QQ: "132434645" }, confirm: 0 },
    { poster: "../../static/images/QQ图片20231213202428.jpg", posterName: "王五", value: '1.本次活动为集体活动，要提前10分钟到达集合地，不要迟到;午饭请自带，但社团亦会准备零食等之类供给大家;另交通费及晚上聚餐费用社团承担。2.因是户外活动，请自备防晒用具;游玩时注意自身安全，尽量不要走散群队。3.请自备相机摄影留念。', month: 2, date: 12, hour: 9, minute: 0, place: '信部操场', person: { personName: "王五", tel: "12674634", QQ: "132434645" }, confirm: 0 },
])

let mineNotice = ref([{ poster: "../../static/images/QQ图片20231213202428.jpg", posterName: "李四", value: '1.本次活动为集体活动，要提前10分钟到达集合地，不要迟到;午饭请自带，但社团亦会准备零食等之类供给大家;另交通费及晚上聚餐费用社团承担。2.因是户外活动，请自备防晒用具;游玩时注意自身安全，尽量不要走散群队。3.请自备相机摄影留念。', month: 3, date: 3, hour: 9, minute: 0, place: '文理学部桂圆操场', person: { personName: "李四", tel: "12674634", QQ: "132434645" }, confirm: 0 },])
let time, location, event, name, tel, qq

function confirm(confirm_) {

    if (confirm_ == 0) {
        return '待确认'
    }
    else {
        return '已确认'
    }
}

function ifConfirm(confirm_) {
    if (confirm_ == 0) {
        return 'unConfirm'
    }
    else {
        return 'confirmed'
    }
}
let popShow = ref(0)
let month, date, hour, minute, place
function confirmed(item) {
    item.confirm = 1
    popShow.value = 1
    month = item.month
    date = item.date
    hour = item.hour
    minute = item.minute
    place = item.place
}


function stand(time_) {
    let time = ''
    if (time_ < 10) {
        time = '0' + time_

    }
    else {
        time = time_
    }
    return time
}

function addClick() {
    popShow.value = 0
}
let height = ref('60px')
let width = ref('60px')
function startClickPost() {
    height.value = '63px'
    width.value = '63px'
}
function endClickPost() {
    height.value = '60px'
    width.value = '60px'
}
let deg = ref(0)
let showAddNotice = ref('')
let hide = ref('hideAddNotice')
function clickPost() {
    if (deg.value == 0) {
        deg.value = 20
        setTimeout(() => { deg.value = 45 }, 50)
        showAddNotice.value = 'showAddNotice'
        hide.value = ''

    }
    if (deg.value == 45) {
        deg.value = 25
        setTimeout(() => { deg.value = 0 }, 50)
        showAddNotice.value = ''
        hide.value = 'hideAddNotice'
        hideContent.value = 'hide'
    }
}

let hideContent = ref('hide')
function showcontents() {
    hideContent.value = ''
}


function postNotice() {
    let minutes
    if (parseInt(time.split('：')[1])) {
        minutes = parseInt(time.split('：')[1])
    }
    else if (parseInt(time.split(':')[1])) {
        minutes = parseInt(time.split(':')[1])

    }
    if (!modify) {

        notice.value.splice(0, 0, { poster: "../../static/images/QQ图片20231213202428.jpg", posterName: name, value: event, month: parseInt(time.split('.')[0]), date: parseInt(time.split('.')[1]), hour: parseInt(time.split(' ')[1]), minute: minutes, place: location, person: { personName: name, tel: tel, QQ: qq }, confirm: 0 })
    }
    else {
        let index = notice.value.indexOf(thisItem)
        console.log(event)
        notice.value.splice(index, 1, { poster: "../../static/images/QQ图片20231213202428.jpg", posterName: name, value: event, month: parseInt(time.split('.')[0]), date: parseInt(time.split('.')[1]), hour: parseInt(time.split(' ')[1]), minute: minutes, place: location, person: { personName: name, tel: tel, QQ: qq }, confirm: 0 })

    }
    time = ''
    location = ''
    event = ''
    name = ''
    tel = ''
    qq = ''
    clickPost()


}

let postContent = ref('total')
function checkMinePost() {
    postContent.value = 'mine'
    clickPost()
}
function checkAllPost() {
    postContent.value = 'total'
    clickPost()
}

let modify = false
let thisItem
function modifyPost(item) {
    thisItem = item
    clickPost()
    time = `${item.month}.${item.date} ${stand(item.hour)}:${stand(item.minute)}`
    location = item.place
    event = item.value
    name = item.person.personName
    console.log(name)
    tel = item.person.tel
    qq = item.person.QQ
    modify = true
    hideContent.value = ''
}
function deletePost(item){
    console.log(item)
    console.log(notice.value.indexOf(item))
    notice.value.splice(notice.value.indexOf(item),1)
}

</script>


<style scoped>
.total {
    display: flex;
    flex-direction: column;
    align-items: center;
    background-color: rgba(187, 232, 255, 0.48);
    min-height: 100vh;
    width: 100vw;
}

.title {
    top:0;
    font-size: 20px;
    background-color: rgb(253, 253, 253);
    width: 100%;
    display: flex;
    justify-content: center;
    padding-top: 10px;
    padding-bottom: 10px;
    position: fixed;

}

.body {
    margin-top: 35px;
    overflow: hidden;
}

.notice {
    border: solid 2px;
    border-color: rgb(188, 188, 188);
    border-radius: 15px;
    margin: 3%;
    margin-top: 20px;
    box-shadow: -2px 2px 2px rgb(202, 202, 202);
    background-color: rgb(255, 255, 255);
}

.dot {
    position: absolute;
    height: 15px;
    width: 15px;
    transform: translate(-4px, -4px);
    background-color: red;
    border-radius: 50%;
    box-shadow: -1px 1px 4px rgb(156, 63, 63);
}

.poster {
    display: flex;
    flex-direction: row;
    align-items: center;
}

.photo {
    height: 48px;
    width: 48px;
    border-radius: 10px;
    margin: 15px;
    margin-top: 0;
    margin-top: 15px;
}


.content {
    font-size: 15px;
    margin-right: 10px;
}


.listBody {
    display: flex;
    flex-direction: column;

}

.listLine {
    display: flex;
    flex-direction: row;
    margin-bottom: 10px;
    margin-left: 15px;
}

.icon {
    height: 20px;
    width: 20px;
    margin-right: 5px;
}

.unConfirm {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 54px;
    transform: translate(240px, 0);
    padding: 3px;
    border-radius: 5px;
    background-color: red;
    color: rgb(255, 255, 255);
    margin-top: 8px;
    margin-bottom: 15px;
    font-size: 14px;
}

.confirmed {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 54px;
    transform: translate(240px, 0);
    padding: 3px;
    border-radius: 5px;
    background-color: rgb(170, 170, 170);
    margin-top: 8px;
    margin-bottom: 15px;
    font-size: 14px;
}

.pop {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    background-color: rgba(252, 252, 252, 0.5);
}

.popChild {
    position: fixed;
    height: 25%;
    width: 54%;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    margin: auto;
    background-color: rgb(255, 255, 255);
    padding: 15px;
    border-radius: 8px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    box-shadow: 0 0 12px rgb(85, 85, 85);
}

.addTodo {
    margin-top: 10px;
    padding: 5px;
    padding-left: 10px;
    padding-right: 10px;
    border-radius: 5px;
    background-color: rgb(40, 183, 255);
    color: rgb(255, 255, 255);
    font-size: 15px;

}

.postNotice {
    background-color: rgb(0, 115, 255);
    border-radius: 50%;
    height: 60px;
    width: 60px;
    position: fixed;
    bottom: 0;
    right: 0;
    transform: translate(-24px, -540px);
    display: flex;
    align-items: center;
    justify-content: center;
    transform: rotate(45);

}


.hideAddNotice {
    display: none;
}

.showAddNotice {
    position: fixed;
    bottom: 0;
    background-color: rgb(201, 234, 255);
    width: 100vw;
    right: 0;
    height: 500px;
    border-top-right-radius: 40px;
    border-top-left-radius: 40px;

}


.addNoticeTop {
    padding: 20px;
    padding-left: 30px;
    padding-right: 30px;
    color: rgb(0, 30, 140);
}

.minePost {
    position: fixed;
    bottom: 0;
    right: 0;
    background-color: rgb(0, 115, 255);
    color: rgb(255, 255, 255);
    padding: 5px;
    border-radius: 5px;
    font-size: 12px;
}

.postBottom {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
}

.postBottomButtom {
    padding: 4px;
    border-radius: 5px;
    background-color: rgb(255, 0, 0);
    color: rgb(255, 255, 255);
    font-size: 12px;
    margin-left: 55px;
    margin-right: 55px;
    margin-bottom: 18px;
}
</style>