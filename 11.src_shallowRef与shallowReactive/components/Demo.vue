<template>
<h4>{{person}}</h4>
<h2>姓名：{{name}}</h2>
<h2>年龄：{{age}}</h2>
<h2>薪资：{{job.j1.salary}}K</h2>
<h2>当前的x值是：{{x.y}}</h2>
<button @click="x.y++">点我x++</button>
<button @click="name+='~'">修改姓名</button>
<button @click="age++">增加年龄</button>
<button @click="job.j1.salary++">涨薪</button>
</template>

<script>
import { ref,reactive,toRefs,shallowRef,shallowReactive } from 'vue'
export default {
  name: 'Demo',
 setup() {

  //  let person = shallowReactive({// 只考虑第一层数据的响应式
   let person = shallowReactive({
    name:'张三',
    age: 20,
    job:{
      j1:{
        salary:20
      }
    }
   })
   let x = shallowRef({
      y:0
   })
   console.log(x);


  
    return {
      person,
      ...toRefs(person),
      x

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
