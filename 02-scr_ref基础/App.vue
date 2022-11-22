<template>
  <h1>一个人的信息</h1>
  <h2>姓名：{{name}}</h2>
  <h2>年龄：{{age}}</h2>
  <h2>工作种类：{{job.type}}</h2>
  <h2>工作薪水：{{job.salary}}</h2>
  <button @click="changInfo">修改人的信息</button>
</template>

<script>
import { ref } from 'vue'
export default {
  name: 'App',
 setup() {
   let name = ref('张三')
   let age = ref(20)
   let job =ref({
    type:'前端工程师',
    salary:'20k'
   })

  function changInfo(){
    name.value = '李四'
    age.value = 18
    console.log(job.value);
    job.value.type = '后端工程师'
    job.value.salary = '50k'
  }
  
    return {
      name,
      age,
      changInfo,
      job
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
