<template>
  <div id="box">
    <header>
      <input type="search" autofocus="autofocus" placeholder="What needs to be done?" v-model="tsval"
        @keydown.enter="enter">
    </header>
    <List :reslist="reslist"></List>
    <footer v-show="reslist.length != 0">
      <span class="todo-count"><strong>{{ reslist.length }}</strong> item left
      </span>
      <ul class="filters">
        <li>All</li>
        <li>Active</li>
        <li>Completed</li>
      </ul>
      <button class="clear-completed" style="display: none;">
        Clear completed
      </button>
    </footer>
  </div>
  <div id="wdo">
    <header id="w-top">

    </header>
    <section id="w-cont">
      <div id="w-pan">
        <p>
          <span class="h">总数：{{ sum }}</span>
        </p>
        <p>
          <span @click="add">
            <span class="l">添加</span>
            <span class="r">+</span>
          </span>
        </p>
      </div>
      <Mobox v-show="nf" @add="(num) => upres(num)" @rem="off"></Mobox>
      <div id="requrst">
        <div class="send" id="shake" @click="req(1)">
          防抖--请求{{ shake }}次
        </div>
        <div class="send" id="thro" @click="req(0)">
          节流--请求{{ thro }}次
        </div>
      </div>
    </section>
  </div>
  <div id="slot">
    <Slot>
      <p>我是默认插槽🎓</p>
      <template v-slot:header>
        <p>我来组成头部😀</p>
      </template>
      <template #section>
        <p>{{ se }}</p>
      </template>
      <template #footer="{ cotxt }">
        <p>{{ cotxt }}</p>
      </template>
    </Slot>
  </div>
{{ a }}
</template>

<script setup>
import { Muesin ,a } from '../utis/Key';
// let a=1
import List from './../components/list.vue'
import { ref } from 'vue'
import Slot from './../components/slot.vue'
let se = '我来组成躯干和手臂🥼'
//需求1
let tsval = ref(null)
let reslist = ref([])
let id = 0
let enter = () => {
  if (!tsval.value) return
  reslist.value.push({ value: tsval.value, id, chen: false, type: 'button' })
  id++
  tsval.value = null
}
//需求二
import Mobox from './../components/mobox.vue'
let sum = ref(0)
let nf = ref(false)
let add = () => {
  nf.value = !nf.value
}
let upres = (num) => {
  sum.value += num
}
let off = () => {
  nf.value = false
}
//防抖节流
let shake = ref(0)
let thro = ref(0)
let timer = null
let timer2 = null
let n = true
let i = 0
let req = (bo) => {
  if (bo) {
    //防抖
    i++
    clearTimeout(timer)
    timer = setTimeout(() => {
      shake.value++
      console.log('点击' + i + '请求一次');
      i = 0
    }, 1000)

  } else {
    //节流
    if (n) {
      thro.value++
      n = !n

    }
    clearTimeout(timer2)
    timer2 = setTimeout(() => {
      n = !n
      console.log(6);
    }, 1000)

  }
}


</script>

<style lang="scss" scoped>
#box {
  width: 550px;
  margin: 60px auto;
  background: #fff;
  box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.2), 0 25px 50px 0 rgba(0, 0, 0, 0.1);

  header {
    width: 100%;
    height: 66px;

    input {
      position: relative;
      margin: 0;
      width: 100%;
      font-size: 24px;
      font-family: inherit;
      font-weight: inherit;
      line-height: 1.4em;
      box-sizing: border-box;
      padding: 16px 16px 16px 60px;
      border: none;
      background: rgba(0, 0, 0, 0.003);
      box-shadow: inset 0 -2px 1px rgba(0, 0, 0, 0.03);
      outline: none;

      &:focus {
        background: #f7f7f7;
        outline: none;
      }

      &[type=search]::-webkit-search-cancel-button {
        -webkit-appearance: none;
        position: relative;
        height: 15px;
        width: 15px;
        border-radius: 50%;
        // background: rgb(248, 135, 135);
        background: #ec5454;
        background-size: 18px 18px;
      }

    }

  }

  footer {
    // width: 100%;
    height: 20px;
    position: relative;
    display: flex;
    flex-wrap: nowrap;
    box-sizing: content-box;
    padding: 10px 15px;
    border-top: 1px solid #e6e6e6;
    text-align: center;
    color: #777;

    .todo-count {
      width: 40%;
      text-align: left;
    }

    .filters {
      width: 60%;
      display: flex;
      flex-wrap: nowrap;
      justify-content: space-around;
      margin: 0;
      padding: 0;
      list-style: none;

      li {
        float: left;
      }
    }

    &::before {
      content: '';
      position: absolute;
      right: 0;
      bottom: 0;
      left: 0;
      height: 50px;
      overflow: hidden;
      box-shadow: 0 1px 1px rgba(0, 0, 0, 0.2), 0 8px 0 -3px #f6f6f6, 0 9px 1px -3px rgba(0, 0, 0, 0.2), 0 16px 0 -6px #f6f6f6, 0 17px 2px -6px rgba(0, 0, 0, 0.2);
    }


  }

}

#wdo {
  width: 750px;
  height: 530px;
  box-shadow: 0 0 6px 1px #16161659;
  margin: 0 auto;
  border-radius: 2px;
  overflow: hidden;

  #w-top {
    width: 100%;
    height: 30px;
    background: #dbdcfb;
  }

  #w-cont {
    width: 100%;
    height: 500px;
    position: relative;

    #w-pan {
      box-sizing: border-box;
      padding: 5px;

      .h {
        width: 100%;
        border-radius: 0;
      }
    }

    p {
      .h {
        font-size: 22px;
        font-weight: 600;
        color: #A8AAD8;
      }

      >span {
        display: flex;
        width: 80px;
        height: 100%;
        border-radius: 24px;
        overflow: hidden;

        >span {
          width: 50%;
          height: 100%;
          font-size: 14px;
          font-weight: 600;
          text-align: center;
          line-height: 24px;
        }

        .l {
          background: #788CD3;
          color: #96b4c0;
        }

        .r {
          background: #BD9DBC;
          color: #5E8AB2;
        }

      }
    }

    #requrst {
      width: 300px;
      height: 50px;
      position: absolute;
      inset: 0;
      z-index: 1;
      margin: auto;
      display: flex;
      flex-wrap: nowrap;
      justify-content: space-evenly;

      .send {
        width: 130px;
        height: 100%;
        background: #405cfa;
        border-radius: 3px;
        text-align: center;
        line-height: 50px;
        color: #fff;
      }
    }
  }


}

#slot{
  width: 270px;
  height: 150px;
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 30px auto;
  border-radius: 5px;
  text-align: end;
  background: #405cfa;

  p{
    width: 190px;
    font-size: 18px;
    font-weight: 600;
    color: #fff;
  }
}
</style>
