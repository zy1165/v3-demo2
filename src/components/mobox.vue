<template>
    <div id="mod">
        <div id="box">
            <p class="p-r" @click="close">关闭</p>
            <p class="inp">
                <!-- <input type="text" v-model="be" @keydown.enter="enter"> -->
                <input type="text" placeholder="只能输入数字不信你就试试!🤬" v-model="be" @input="put">
            </p>
            <p class="dosum" v-show="dosum > 0">双倍数量：{{ dosum }}</p>
            <p class="fot">
                <span class="but" @click="rem">清空</span>
                <span class="but" @click="add">确认</span>
            </p>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue'

const emit = defineEmits(['add', 'rem'])
let be = ref(null)
let dosum = ref(null)
let enter = () => {
    // console.log(be.value.split('').filter(item=>Number(item)).join(''));
    be.value = be.value.split('').filter(item => Number(item)).join('')
    dosum.value = be.value * 2
}
let put = () => {
    let numval = ref(null)
    if (be.value.split('').filter(item => item == '.').length > 1) {
        numval.value = be.value.split('').filter(item => Number(item) || item == 0)
        // console.log(numval.findIndex(item=>Number(item)));
        numval.value.push('.')
        // console.log(numval.value);
    } else {
        numval.value = be.value.split('').filter(item => Number(item) || item == 0 || item == '.')
        // console.log([...numval.value]);
    }
    let ult = numval.value.findIndex(item => Number(item) || item == '.')
    if (ult < 0) ult = 1
    // console.log(ult);
    be.value = numval.value.splice(ult).join('')
    dosum.value = be.value * 2
}
let rem = () => {
    be.value = null
    dosum.value = null
}
let add = () => {
    if (!dosum.value) return
    emit('add', dosum.value)
    be.value = null
    dosum.value = null
}
let close = () => {
    emit('rem')
}


</script>

<style lang="scss" scoped>
#mod {
    width: 100%;
    height: 100%;
    position: absolute;
    top: 0;
    z-index: 99;
    background: #00000060;

    #box {
        width: 300px;
        height: 350px;
        position: absolute;
        inset: 0;
        margin: auto;
        box-sizing: border-box;
        padding: 15px;
        border-radius: 20px;
        background: #fff;
        font-size: 16px;

        p {
            width: 100%;

        }

        .p-r {
            margin-bottom: 10px;
            text-align: right;
            font-size: 14px;
        }

        .inp input {
            width: 200px;
            height: 25px;
            display: block;
            margin: 0 auto;
        }

        .dosum {
            margin: 5px 10px;
            font-weight: 600;

        }

        .fot {
            margin-top: 10px;
            display: flex;
            flex-wrap: nowrap;
            justify-content: space-around;

            .but {
                width: 65px;
                height: 30px;
                border-radius: 2px;
                background: rgb(68, 159, 250);
                text-align: center;
                line-height: 30px;
                font-weight: 600;
            }
        }
    }

}
</style>