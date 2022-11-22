<template>
<h2>当前的求和为：{{sum}}</h2>
<button @click="sum++">点我加1</button>
<br>
<h2>当前的信息为：{{msg}}</h2>
<button @click="msg+='!'">修改信息</button>
<hr>
<h2>姓名：{{person.name}}</h2>
<h2>年龄：{{person.age}}</h2>
<h2>薪资：{{person.job.j1.alary}}K</h2>
<button @click="person.name+='~'">修改姓名</button>
<button @click="person.age++">增加年龄</button>
<button @click="person.job.j1.alary++">涨薪</button>
</template>

<script>
import { ref,watch,reactive } from 'vue'
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
 
    // 监视 (情况1) 监视ref所定义的一个响应式数据
    watch(sum,(newValue,oldValue)=>{
      console.log(newValue,oldValue);
    },{immediate:true})

    // 监视 (情况2)监视ref所定义的多个响应式数据
    watch([sum,msg],(newValue,oldValue)=>{
      console.log(newValue,oldValue);
    })

    // 监视 (情况3) 监视reactive所定义的一个响应式数据 
    // 1.此处无法正确的获取oldValue
    // 2.强制开启了深度监视(deep配置无效)
     watch(person,(newValue,oldValue)=>{
      console.log('person变化了',newValue,oldValue);
    },{deep:false})// 此次的deep:false无效

    // 监视 (情况4) 监视reactive所定义的一个响应式数据中的某个属性
    watch(()=>person.age,(newValue,oldValue)=>{
      console.log('person的age变化了',newValue,oldValue);
    })

    // 监视 (情况5) 监视reactive所定义的一个响应式数据中的某些属性
    watch([()=>person.age,()=>person.name],(newValue,oldValue)=>{
      console.log('person的age或name变化了',newValue,oldValue);
    })

    // 特殊情况
    watch([()=>person.job],(newValue,oldValue)=>{
      console.log('person的jbo变化了',newValue,oldValue);
    },{deep:true})// 此处由于监视的是reactive属性定义的对象中的某个属性，所以deep有效

  
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
