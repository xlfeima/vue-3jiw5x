<template>
  <button @click="modalOpen=true">
  弹出一个模态窗口
  </button>
  <teleport to='body'>
  <div v-if="modalOpen" class="modal">
  <div>
  这是一个弹窗 我的父元素是 <body>
    <button @click="modalOpen=false">关闭</button>
  </body>
  </div>
  </div>
  </teleport>
</template>
<script>
export default{
  data(){
     return {
       modalOpen:true
     }
  }
}
</script>
