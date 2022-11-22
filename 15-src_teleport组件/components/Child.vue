<template>
  <div class="Child">
    <h3>我是Child组件</h3>
    <Son/>
  </div>
</template>

<script>
import Son from './Som'
export default {
  name:'Child',
  components:{Son},
}
</script>

<style>
.Child{
  background-color: rgb(81, 158, 202);
  padding: 10px;
}
</style>