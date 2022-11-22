<template>
  <div class="Som">
    <h3>我是Son组件</h3>
    <Dialog/>
  </div>
</template>

<script>

import Dialog from './Dialog'
export default {
  name:'Som',
  components:{Dialog}
}
</script>

<style>
.Som{
  background-color: rgb(217, 16, 180);
  padding: 10px;
}
</style>