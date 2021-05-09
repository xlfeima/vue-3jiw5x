<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>{{counter}}
    </p>
     <p>{{doubleCounter}}
    </p>
    <p ref="desc">
    </p>
  </div>
    <ModalButton></ModalButton>
</template>

<script>
import {reactive,computed,onMounted,onUnmounted,ref,toRefs,watch} from 'vue'
import  ModalButton from './ModalButton.vue'

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  //注册组件
  components:{
    ModalButton
  },
  setup(){

    //counter 相关
    const {counter,doubleCounter}=  useCounter();

   //其他数据单值响应
    const msg2=ref('some massage');;

   //使用元素引用
    const desc=ref(null);

    //侦听器
    watch(counter,(val,oldVal)=>{
    debugger
    const p=desc.value;
    p.textContent= ' counter change from ' +oldVal+ ' to ' +val;
    })
    return {counter,doubleCounter,msg2,desc};
  }
};

///定时counter
function useCounter(){

 const data= reactive({
          counter:1,
          doubleCounter:computed(()=>data.counter*2),
    });

    let timer;

    onMounted(()=>{
     timer= setInterval(()=>{
      data.counter++
      },1000);
    });

    onUnmounted(()=>{
      clearInterval(timer);
    });
    return toRefs(data);
}
</script>

