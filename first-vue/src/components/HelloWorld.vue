<template>
    <div class="header" :class="{box: true}">
        <img src="../assets/WSL.png">
        <ul>
            <li
                v-for="(value,key) in top_selection" 
                class="nav" 
                @mouseover.self="mouse_over" 
                @mouseleave.self="mouse_leave"> 
                {{key}} 
                <Transition>
                    <div v-if="top_selection[key].show" class="popdown">
                        <ul>
                            <li v-for="item in top_selection[key].items">
                                    {{item}}
                            </li>
                        </ul>
                    </div>
                </Transition>
            </li>
        </ul>
        <div>
            <input>search
        </div>
    </div>
    <div v-if="false" class="body" :class="{box: true}">
        <h1>{{ props.msg }}</h1>
    </div>
    
</template>


<script setup lang="ts">
import {ref} from 'vue'
interface NavItem {
    show: boolean;
    items: string[];
}
interface SelectionStructure {
    [key: string]: NavItem;
}

const props = defineProps(['msg'])
const top_selection= ref<SelectionStructure>({
    'About me': {show: false, items: ['email','tg']},
    'Roadmap': {show: false, items: ['plan','next']},
    'Record':{show: false, items: ['github']},
    'Achievement':{show: false, items: ['showcase']}
})

function mouse_over(event: MouseEvent){
    if(event.target === null)return;
    let key: string = (event.target as HTMLElement).innerText.split('\n')[0] || '';
    top_selection.value[key]['show'] = true
}

function mouse_leave(event: MouseEvent){
    if(event.target === null)return;
    let key: string = (event.target as HTMLElement).innerText.split('\n')[0] || '';
    top_selection.value[key]['show'] = false
}

</script>

<style scoped>
* {
    color: white;
}

.header img {
    height: 80%;
    pointer-events: none;
}

.header>ul>li {
    list-style: none;
    width: 25%;
    text-align: center;
    height: 100%;
    line-height: 60px;
}

.popdown{
    position: absolute;
    top: 100%;
    background-color: pink;
    width: 10%;
    height: 60px;
}


.header input{
    /* height: 30%; */
    margin: 0px auto;
    width: 75%;
}


.header>ul{
    width: 40%;
    padding: 0px;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
}

.show{
    height: 100px;
    background-color: azure;
}

.body{
    background-color: azure;
}

.box{
    box-sizing: border-box;
    width: 80%;
    margin: 0px auto;
    /* overflow: hidden; */
}

.header{
    width: 100%;
    height: 60px;
    display: flex;
    background-color: rgba(0,0,0,0.5);
    backdrop-filter: blur(10px);
    box-shadow: 0px 5px 5px rgba(0,0,0,0.2);
    justify-content: center;
    align-items: center;
    position: relative;
}

.nav:hover{
    /* background-color: rgba(255,255,255,0.4); */
    /* backdrop-filter: blur(10px); */
    box-shadow: 0px 0px 10px 10px rgba(0,0,0,0.2);
    /* color: pink; */
}

/* we will explain what these classes do next! */
.v-enter-active,
.v-leave-active {
  transition: opacity 0.35s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}

</style >
