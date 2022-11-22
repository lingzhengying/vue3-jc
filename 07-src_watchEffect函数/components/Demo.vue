<template>
<h2>当前的求和为：{{sum}}</h2>
<button @click="sum++">点我加1</button>
<br>
<h2>当前的信息为：{{msg}}</h2>
<button @click="msg+='!'">修改信息5</button>
<hr>
<h2>姓名：{{person.name}}</h2>
<h2>年龄：{{person.age}}</h2>
<h2>薪资：{{person.job.j1.alary}}K</h2>
<button @click="person.name+='~'">修改姓名</button>
<button @click="person.age++">增加年龄</button>
<button @click="person.job.j1.alary++">涨薪</button>
</template>

<script>
import { ref,watch,reactive,watchEffect } from 'vue'
export default {
  name: 'Demo',
 setup() {

   let sum = ref(0)
   let msg = ref('你好呀')
   let person = reactive({
    name:'张三',
    age: 20,
    job:{
      j1:{
        alary:20
      }
    }
   })
    // // 监视
    //   watch(msg,(newValue,oldValue)=>{
    //     console.log('msg的值改变了',newValue,oldValue);
    //   },{immediate:true})
  

  watchEffect(()=>{
    const x1 = sum.value
    const x2 = person.age
    console.log('watchEffect所指定的回调执行了',x1,x2);
  })
  
    return {
      msg,
      sum,
      person
    }
 }

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
