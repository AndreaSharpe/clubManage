<template>
    <div class="page">
        <div class="top">
            <img src="../static/images/home.svg" style="width: 24px;height: 24px;">
            <div>近期待办</div>

            <div>
                <div v-show="ifShow">
                    <div class="selectChoice" @click="clickTotal" :style="buttonStyle1">全部</div>
                    <div class="selectChoice" @click="clickComplete" :style="buttonStyle2">已完成</div>
                </div>
                <img src="../static/images/select.svg" class="selectButton" @click="clickSelect">
            </div>
        </div>
        <div style="overflow-y: scroll;max-height:470px">
            <div class="body" v-for="item in index">
                <div class="task">
                    <img src="../static/images/圆形未选中.svg" :class="ifChosen1[item]" @click="changeButton(item)">
                    <img src="../static/images/圆形选中.svg" :class="ifChosen2[item]" @click="changeButton(item)">
                    <div class="listBody">
                        <div class="listLine">
                            <img v-if="grey[item] == ''" src="../static/images/time.svg" class="icon">
                            <img v-else src="../static/images/timeGrey.svg" class="icon">

                            <div :class="'content ' + grey[item]" style="margin: 3px;">{{ list[item].month }}.{{
                                list[item].date }}</div>
                            <div :class="'content ' + grey[item]">{{ stand(list[item].hour) }}:{{ stand(list[item].minute)
                            }}</div>
                        </div>
                        <div class="listLine">
                            <img v-if="grey[item] == ''" src="../static/images/location.svg" class="icon">
                            <img v-else src="../static/images/locationGrey.svg" class="icon">
                            <div :class="'content ' + grey[item]" style="width: 230px;">{{ list[item].place }}</div>
                            <div :class="'content ' + grey[item]" style="font-size: 10px;">还剩1天</div>

                        </div>
                        <div class="listLine">
                            <img v-if="grey[item] == ''" src="../static/images/list.svg" class="icon">
                            <img v-else src="../static/images/listGrey.svg" class="icon">
                            <div :class="'content ' + grey[item]" style="width: 230px;">{{ list[item].value }}</div>
                            <div :class="list[item].important">重要</div>
                        </div>

                    </div>


                </div>

            </div>
        </div>

        <div style="width:340px;height:20%;" @click="cancelAdd"></div>
        <div :class="'add ' + active" @click="changeAdd">
            <div style="font-size: 15px;padding-left:8px;" :class="addBefore">+ 添加待办</div>
            <div :class="addAfter + ' addTip'">
                <img src="../static/images/圆形未选中.svg" class="chosen">
                <div class="listBody">
                    <div class="listLine">
                        <img src="../static/images/time.svg" class="icon">
                        <input class="addText content" style="margin: 3px;" placeholder="此处添加时间" v-model="time" />
                    </div>
                    <div class="listLine">
                        <img src="../static/images/location.svg" class="icon">
                        <input class="addText content" placeholder="此处添加地点" style="width:230px;" v-model="location" />
                        <div @click="changeImportant" :class="important" style="margin-top:6px;">重要</div>

                    </div>
                    <div class="listLine">
                        <img src="../static/images/list.svg" class="icon">
                        <input class="addText content" placeholder="此处添加地点" style="width:240px;" v-model="event" />
                        <div class="submit" @click="submit">确定</div>
                    </div>

                </div>




            </div>
        </div>
    </div>
</template>
<script setup>
import { ref } from 'vue'
let list = ref([{ value: '洗鞋子', month: 2, date: 5, hour: 9, minute: 0, finish: 0, important: 'importantActive', place: '文理学部桂圆操场' }, { value: '报道', month: 2, date: 7, hour: 15, minute: 0, finish: 0, important: 'important', place: '文理学部桂圆操场' }, { value: '开学',  month: 2, date: 6, hour: 15, minute: 0, finish: 0, important: 'important', place: '文理学部桂圆操场' }, { value: '生日', month: 2, date: 4, hour: 15, minute: 0, finish: 0, important: 'important', place: '文理学部桂圆操场' }])
let listCopy = ref([])
let ifImportant = false
let index = ref([])
let indexCopy = []
let flagButton = ref(0)
let ifChosen1 = ref([])
let ifChosen2 = ref([])

let grey = ref([])
let ifShow = ref('')
let active = ref('')
for (let i = 0; i < list.value.length; i++) {
    grey.value.push('')
    ifChosen1.value.push('chosen')
    ifChosen2.value.push('unChosen')
    index.value.push(i)
}

let time = ref()
let event = ref()
let location = ref()

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


function clickSelect() {
    ifShow.value = !ifShow.value
}

let unSelect = "background-color: rgb(255, 255, 255);color: rgb(0, 0, 0)"
let selected = "background-color: #135784;color: rgb(255, 255, 255);"
let buttonStyle1 = ref()
buttonStyle1.value = selected
let buttonStyle2 = ref()
buttonStyle2.value = unSelect

function clickTotal() {
    if (buttonStyle1.value == unSelect) {
        buttonStyle1.value = selected
        buttonStyle2.value = unSelect
        console.log(index.value.length)
        let len = index.value.length
        for (let k = 0; k < indexCopy.length; k++) {
            if (k < len) {
                index.value[k] = indexCopy[k]
            }
            else {
                index.value.push(indexCopy[k])
            }
        }

    }

}

function clickComplete() {
    if (buttonStyle2.value == unSelect) {
        buttonStyle2.value = selected
        buttonStyle1.value = unSelect
        indexCopy = indexCopy.splice(indexCopy.length)
        for (let k = 0; k < index.value.length; k++) {
            indexCopy.push(index.value[k])
        }

        let j = index.value.length
        for (let i = 0; i < index.value.length; i++) {
            if (list.value[index.value[i]].finish == 1) {
                j = i
                break
            }

        }
        index.value = index.value.splice(j)
    }



}

for (let i = 0; i < list.length; i++) {
    if (list.value[i].finish == 0) {
        ifChosen1.value[i] = 'chosen'
    }
    else {
        ifChosen1.value[i] = 'unChosen'
    }
}

function sort() {
    for (let i = 0; i < list.value.length - 1; i++) {
        for (let j = i + 1; j < list.value.length; j++) {
            if (list.value[i].month > list.value[j].month || (list.value[i].month == list.value[j].month && list.value[i].date > list.value[j].date)) {
                let x = index.value[i]
                index.value[i] = index.value[j]
                index.value[j] = x
            }
        }
    }
}
sort()
console.log(index.value)
// console.log(index.value)


function changeButton(item) {
    console.log(item)

    // console.log(finish)

    if (list.value[item].finish == 1) {
        console.log('hh')
        ifChosen1.value[item] = 'chosen'
        ifChosen2.value[item] = 'unChosen'
        let x
        for (let i = 0; i < index.value.length; i++) {
            if (index.value[i] == item) {
                x = i
                break
            }
        }
        let flag = false
        let hold, temporary
        for (let j = 0; j < x + 1; j++) {
            if (flag) {
                temporary = index.value[j]
                index.value[j] = hold
                hold = temporary
            }
            if (flag == false && (list.value[index.value[j]].finish == 0 && (list.value[index.value[j]].month > list.value[item].month || (list.value[index.value[j]].month == list.value[item].month && list.value[index.value[j]].date > list.value[item].date)))) {
                hold = index.value[j]
                index.value[j] = item
                flag = true
            }
            else if (flag == false && list.value[index.value[j]].finish == 1) {
                hold = index.value[j]
                index.value[j] = item
                flag = true
            }

        }

        grey.value[item] = ''
    }
    else {
        let t = index.value.length - 1
        ifChosen1.value[item] = 'unChosen'
        ifChosen2.value[item] = 'chosen'
        for (let k = 0; k < index.value.length - 1; k++) {
            if (index.value[k] == item || (k != 0 && index.value[k - 1] == index.value[k])) {
                index.value[k] = index.value[k + 1]
            }
            if (list.value[index.value[k + 1]].finish == 1) {
                t = k
                break
            }
        }
        let flag = false
        for (t; t < index.value.length - 1; t++) {
            if (list.value[index.value[t + 1]].month > list.value[item].month || (list.value[index.value[t + 1]].month == list.value[item].month && list.value[index.value[t + 1]].date > list.value[item].date)) {
                index.value[t] = item
                flag = true
                break
            }
            else {
                index.value[t] = index.value[t + 1]

            }
        }
        if (flag == false) {
            index.value[index.value.length - 1] = item
        }

        grey.value[item] = 'grey'
    }
    console.log(index.value)
    // let finish= list.value[item].finish
    // finish = 1-finish
    list.value[item].finish = 1 - list.value[item].finish
}

let important = ref('important')
function changeImportant() {
    if (important.value == 'important') {
        important.value = 'importantActive'
    }
    else {
        important.value = 'important'
    }
}
let addBefore = ref("")
let addAfter = ref("addHide")

function changeAdd() {
    addBefore.value = 'addHide'
    addAfter.value = ''
    active.value = 'task'

}

function cancelAdd() {
    addBefore.value = ''
    addAfter.value = 'addHide'
    active.value = ''
    console.log('jlk')
}

function submit() {
    let month = parseInt(time.value.split('.')[0])
    let date = parseInt(time.value.split('.')[1])
    let hourMinute = time.value.split(' ')[1]
    console.log(hourMinute)
    let hour = parseInt(hourMinute.split(':')[0])
    let minute = parseInt(hourMinute.split(':')[1])


    let newContent = { value: event.value, key: '1', month: month, date: date, hour: hour, minute: minute, finish: 0, important: important.value, place: location.value }
    list.value.push(newContent)
    index.value.push(list.value.length - 1)
    grey.value.push('')
    ifChosen1.value.push('chosen')
    ifChosen2.value.push('unChosen')
    let item = index.value.length - 1
    let flag = false
    let hold, temporary
    for (let j = 0; j < index.value.length; j++) {
        if (flag) {
            temporary = index.value[j]
            index.value[j] = hold
            hold = temporary
        }
        if (flag == false && (list.value[index.value[j]].finish == 0 && (list.value[index.value[j]].month > list.value[item].month || (list.value[index.value[j]].month == list.value[item].month && list.value[index.value[j]].date > list.value[item].date)))) {
            hold = index.value[j]
            index.value[j] = item
            flag = true
        }
        else if (flag == false && list.value[index.value[j]].finish == 1) {
            hold = index.value[j]
            index.value[j] = item
            flag = true
        }

    }
    time.value = ''
    event.value = ''
    important.value = 'important'
}


</script>

<style scoped>
.top {
    display: flex;
    flex-direction: row;
    margin: 10px;
    margin-right: 200px;
    margin-top: 20px;
}

.selectButton {
    position: absolute;
    transform: translate(190px, 1px);
    height: 20px;
    width: 20px;
}

.selectChoice {
    font-size: 8px;
    position: absolute;
    border-radius: 4px;
    width: 30px;
    height: 14px;
    display: flex;
    align-items: center;
    justify-content: center;


}

.selectChoice:nth-child(2) {
    transform: translate(150px, 10px);
}

.selectChoice:nth-child(1) {
    transform: translate(150px, -8px);
}

.body {
    width: 340px;

}

.page {
    position: absolute;
    height: 100vh;
    background-color: rgba(207, 239, 255, 0.48);
    width: 100vw;
    display: flex;
    flex-direction: column;
    align-items: center;


}

.task {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: start;
    margin-bottom: 8px;
    background-color: rgb(255, 255, 255);
    border-radius: 5px;
    padding-top: 5px;
    padding-bottom: 5px;
}

.chosen {
    position: relative;
    width: 18px;
    height: 18px;
    margin: 8px;
}

.unChosen {
    display: none;
}

.content:nth-child(1) {
    font-size: 15px;
}

.content:nth-child(2) {
    font-size: 15px;
}

.content:nth-child(4) {
    font-size: 11px;
}

.listBody {
    display: flex;
    flex-direction: column;
    width: 320px;

}

.listLine {
    display: flex;
    flex-direction: row;
    height: 30px;
    align-items: center;
}

.icon {
    height: 20px;
    width: 20px;
    margin-right: 5px;
}

.grey {
    color: gray;
}

.add {
    width: 340px;
    position: absolute;
    transform: translate(0, 550px);
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: start;
    padding-bottom: 8px;
    padding-top: 8px;

    background-color: rgb(255, 255, 255);
    border-radius: 5px;
}

.addTip {
    display: flex;
    flex-direction: row;
    align-items: center;
}

.addText {
    width: 100px;
    height: 30px;
    margin-right: 4px;
}

.addHide {
    display: none;
}

.submit {
    font-size: 12px;
    width: 25px;
}

.important {
    font-size: 11px;
    border: solid 1px;
    border-radius: 4px;
    border-color: rgb(196, 196, 196);
    padding: 2px;
    margin-left: 8px;
    height: 16px;

}

.importantActive {
    font-size: 12px;
    border: solid 1px;
    border-radius: 4px;
    padding: 2px;
    margin-left: 8px;
    background-color: rgb(243, 24, 24);
    color: rgb(255, 255, 255);
    height: 16px;


}</style>
