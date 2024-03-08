<template>
<div style="display: flex;flex-direction:column;"> 
    <div class="search" v-if="searchShow" style="display: flex;flex-direction:column;align-items:center;">
        <div class="cutLine"></div>
        <div style="display: flex;flex-direction:row;padding-top:5px;transform:translate(-7px,0);align-items:center;">
            <img src="../static/images/search.svg" style="width: 16px;height: 16px;padding-right:5px;">
            <div class="erect"></div>
            <input type="text" placeholder="搜索" v-model="clubName" @input="inputChanged" style="width: 220px;font-size:12px;"/>
        </div>
        <div class="cutLine"></div>
        <div class="clubs">
            <div v-for="club in clubs" v-if="clubName!=''">
                <div v-if="clubName==club.name" class="club" @click="clubAdd(club)">
                    <div class="erect"></div>
                    <text>{{club.name}}</text>
                </div>
            </div>
            <div v-else v-for="club in clubs" class="club" @click="clubAdd(club)" >
                <div class="erect"></div>
                <text>{{club.name}}</text>
            </div>
        </div>
    </div>
    <div style="display: flex;flex-direction:row;overflow-x: scroll;width:230px;height: 25px;white-space: nowrap;align-items:center;" @click.stop="choseClub">
        <div v-if="chosen" v-for="club in clubChosen" :key="club.id" class="chosenDisplay" @click="searchHide" @click.stop="choseClub">
            <div class="chosenClub">
                <p style="font-size:12px;">{{ club.name }}</p>
                <div class="icon" @click="clearIcon(club.name)">
                    <img src="../static/images/deleteB.svg" style="width: 8px;height: 8px;">
                </div>
            </div>
            
        </div>
        
        <div v-else style="color: rgb(143, 143, 143);padding-left:5px;font-size:10px;font-family: PingFangSC-regular;">请选择</div>
    </div>
    
</div>   
</template>

<script setup>
    import {ref,defineExpose} from 'vue'
    
    

    let clubs = [{name:'戏剧社',id:0},{name:'推理社',id:1},{name:'文学社',id:2},{name:'书法社',id:3}]
    let clubChosen = ref([])
    let clubName = ref('')
    let chosen = ref(false)
    let searchShow = ref(false)

    defineExpose({searchShow(res){
        searchShow.value = res
    }})

    function choseClub(){
        if(searchShow.value == true){
            searchShow.value = false
        }
        else{
            searchShow.value = true
        }
        
    }
    function searchHide(){

        searchShow.value = false
    }
    function clearIcon(clubName){
        let j = 0;
        for(let i = 0;i<clubChosen.value.length;i++){
            if(clubChosen.value[i].name==clubName){
                i++
            }
            if(i<clubChosen.value.length){
                clubChosen.value[j] = clubChosen.value[i]
                j++
            }
            
        }
        clubChosen.value = clubChosen.value.slice(0,j)
        if(j==0){
            chosen.value = false
        }
        console.log(clubChosen.value)
    }


    function clubAdd(club){
        clubChosen.value.push(club)
        console.log(clubChosen.value)
        chosen.value = true
        searchShow.value = true
        clubName.value = ''
    }


</script>

<style scoped>
    .chosenDisplay{
        display: flex;
        align-items: center;
        padding-left: 6px;
        height: 25px;
    }

    .chosenClub{
        height: 15px;
        background-color: rgb(195, 195, 195);
        padding: 4px;
        border-radius: 5px;
        display: flex;
        flex-direction: row;
    }

    .icon{
        width: 14px;
        height: 14px;
        display: flex;
        align-items: center;
        justify-content: center;
        padding: 2px;
    }

    .cutLine{
        width: 260px;
        height: 0px;
        background-color: rgba(187,187,187,1);
        border: 1px solid rgba(187,187,187,1);
        margin-top: 3px;
    }

    .search{
        width: 292px;
        max-height: 200px;
        background-color: #efefef;
        position: absolute;
        transform: translate(-45px,25px);
        border-bottom-left-radius: 16px;
        border-bottom-right-radius: 16px;
        display: flex;
        flex-direction:column;
        align-items:center;
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


    .clubs{
        display: flex;
        flex-wrap: wrap;
        padding-left: 30px;
        margin: 5px;
    }
    .club{
        height: 20px;
        min-width: 120px;
        display: flex;
        align-items: center;
    }

    .club text{
        background-color: rgb(195, 195, 195);
        padding: 1px;
        padding-left: 6px;
        padding-right: 6px;
        border-radius: 5px;
        font-size: 12px;
    }
</style>