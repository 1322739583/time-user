<script setup>
import {getCurrentInstance, onMounted, ref} from "vue";
//时间块
let blocks = ref([
     // {id:1,select:false,color:"#ffccff"}
])
let colors=ref(["#ffebcc","#18ca24","#1870ca"])
const defaultColor="#cccccc"
const selectColor="#9c9999"
let clockCount=ref(2)//每小时几个时间块
const clickColor=(color)=> {
  console.log("color:",color)
  console.log("App.vue clickColor blocks:", blocks.value)
  blocks.value=blocks.value.map(item=>{
    console.log("App.vue item :",item )
    if (item.select){
      return {
        ...item,
        select:false,
        color
      }
    }else {
      return item
    }
  })

  console.log("App.vue clickColor blocks.value :",blocks.value )
 // blocks.value=[...blocks.value]
}
// function clickBlock(item) {
//   console.log("App.vue clickBlock item:", item)
//   blocks.value[item.id].select=!item.select
// }

function clickBlock(clickedItem) {
  blocks.value = blocks.value.map(item => {
    if (item.id === clickedItem.id) {
      return { ...item, select: !item.select ,color:selectColor};
    }
    return item;
  });
}

onMounted(()=>{
  console.log(24*clockCount.value)
 const arr=[]
  for (let i = 0; i < 24*clockCount.value; i++) {
    arr.push({id:i,color:defaultColor,select:false})
  }
  blocks.value=[...arr]

  // for (const i in 24*clockCount.value) {
  //   console.log("App.vue i :",i )
  //   blocks.value.push({id:i,color:defaultColor,select:false})
  // }


})
</script>

<template>
  <div class="container">
    <div class="time-line-block">
      <div class="time-line-wrapper">
        <div class="time-line" v-for="i in 24">{{ i-1 }}</div>
      </div>
      <div class="block-wrapper">
<!--        {{blocks.length}}-->
        <div :class="item.select?'blocked':'block'" :style="{background:item.color}" v-for="item in blocks" @click="clickBlock(item)" :key="item.id"></div>
      </div>
      <div class="colors-wrapper">
        <div class="color" :style="{background:color}" @click="clickColor(color)" v-for="color in colors" :key="color"></div>
      </div>
    </div>

  </div>
</template>

<style lang="less" scoped>
.container {
  .time-line-block{
    display: flex;
    //background: lightcoral;
    .time-line-wrapper{

      .time-line{
        height: 100px;
        margin-top: 10px;
        line-height: 100px;

      }
    }
    .block-wrapper {
      display: flex;
      flex-wrap: wrap;
      width: 440px;
      background: lightgreen;

      .block {
        width: 200px;
        height: 100px;
        border-radius: 5px;
        margin-left: 5px;
        margin-top: 5px;
        background: #ccc;
      }
      .blocked {
        width: 200px;
        height: 100px;
        border-radius: 5px;
        margin-left: 5px;
        margin-top: 5px;
        background: #9c9999;
      }
    }
    .colors-wrapper{
      .color{
        background: pink;
        width: 200px;
        height: 100px;
      }
    }

  }


}
</style>
