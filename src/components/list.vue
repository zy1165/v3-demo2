<template>
    <section>
        <ul id="uls" v-for="({ value, id, chen, type }, i) in res">
            <li>
                <span :class="['chen', chen ? 'active' : '']" @click="act(id)"></span>
                <input :type="type" v-model="res[i].value" @click="mod(id)" @keydown.enter="enter(id)">
                <span class="rem" @click="rem(id)">X</span>
            </li>

        </ul>
    </section>
</template>

<script setup>
import { ref } from 'vue'

let props = defineProps(['reslist'])
let res = ref(props.reslist)
let act = (id) => {
    //选中
    let i = res.value.findIndex(item => item.id == id)
    res.value[i].chen = !res.value[i].chen
}
let rem = (id) => {
    let i = res.value.findIndex(item => item.id == id)
    res.value.splice(i, 1)
    // console.log(id,i);
}
let mod = (id) => {
    let i = res.value.findIndex(item => item.id == id)
    res.value[i].type = 'search'
    // console.log(55);
}
let enter = (id) => {
    let i = res.value.findIndex(item => item.id == id)
    setTimeout(() => {
        res.value[i].type = 'button'
    }, 0)
    // console.log(66);
}

</script>

<style lang="scss" scoped>
section {
    width: 100%;
    border-top: 1px solid #e6e6e6;

    #uls {
        width: 100%;
        list-style: none;
        padding: 0;

        li {
            width: 100%;
            height: 58px;
            display: flex;
            flex-direction: row;
            flex-wrap: nowrap;
            justify-content: space-between;
            align-items: center;
            box-sizing: border-box;
            padding: 0 10px;
            border-bottom: 1px solid #ededed;

            span {
                display: block;
                width: 23px;
                height: 23px;
                flex-shrink: 0;
                // background: #e04646;
                line-height: 23px;
                text-align: center;
            }

            .chen {
                width: 28px;
                height: 28px;
                // background: lightgreen;
                border: #c7c7c7 1px solid;
                border-radius: 32px;
            }

            .chen.active::before {
                content: '√';
                display: block;
                width: 100%;
                height: 100%;
                font-size: 22px;
                font-weight: 600;
                color: chartreuse;
            }

            .rem {
                background: transparent;
                background: rgb(211, 211, 211);
                border-radius: 100%;
                font-size: 20px;
                font-weight: 600;
                color: #ec5454;
            }

            input {
                width: 100%;
                height: 100%;
                background: #fff;
                border: none;
                outline: none;
                text-align: start;
                font-size: 22px;
            }
        }
    }
}
</style>