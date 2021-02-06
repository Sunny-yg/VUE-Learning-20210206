<template>
  <div>
    <h2>Javascript表达式</h2>
      {{a+1}}  
      <br><br>
      {{flag?name1:name2}}
      <br><br>
      {{message.split("").reverse().join()}}          
      <!-- split 将字符串分割成字符串数组  -->

      <h3>v-if、v-else、v-else-if</h3>
      <div v-if="flag==true">this is true</div>
      <br><br>
      <span v-if="flag==true">this is true</span>
      <span v-else>this is false</span>
      <br><br>
      <div v-if="Math.random()>0.5">大于0.5</div>
      <div v-else>小于0.5</div>
      <br><br>
      <div v-if="type=='A'">A</div>
      <div v-else-if="type=='B'">B</div>
      <div v-else-if="type=='C'">C</div>
      <div v-else>not A/B/C</div>
      <br><br>

      <template v-if="flag">
        <hr> 
        <span>这是一个span</span>
        <div>这是一个div</div>
        <hr>
        <!-- template 可以替换成div,建议使用template，hr代表横线 -->
      </template>
      <br><br>
      <h3>v-if与v-show</h3>
      <div>
        <h4 v-if="flag==true">v-if显示</h4>
        <h4 v-if="flag==true">v-show显示</h4>

      </div>

      <h3>计算属性</h3>
      <div>
        {{reverseMsg}}
        <br><br>
        <button @click="setMsg()">改变msg的值</button>
        <br><br>
        <input type="text" v-model="keyword" placeholder="请输入关键字"/>
        <ul>
          <li v-for="(item,index) in searchData" :key="index">{{item}}</li>
        </ul>
        <br><br>
      </div>
      <h3>watch监听数据变化</h3>
      <div>
        <input type="text" v-model="firstName" placeholder="firstName">
        <br><br>
        <input type="text" v-model="lastName" placeholder="lastName">
        <!-- 方式一：通过计算属性监听   -->
        {{fullNameFn}} 
        <br><br>
        <!-- 方式二：通过watch监听 -->
        {{fullName}}

      </div>
      
  </div> 
      
</template>

<script>
export default {
  data() {
    return {
      a:12,
      flag:false,
      message:"三国演义",
      name1:"张三",
      name2:"李四",
      type:"B",
      listaData:['apple','bannana','orange','pear'],
      keyword:"",
      firstName:"",
      lastName:"",
      fullName:""     

      }

    },
     methods:{
    setMsg(){
      this.message="大家好";
    }

  },
  computed:{
    reverseMsg(){
      return this.message.split("").reverse().join("");

    },
    searchData(){
      var temArr=[];
      this.listaData.forEach((value)=>{
        if(value.indexOf(this.keyword) !=-1 && this.keyword!=""){
          temArr.push(value);

        }
      })
      return temArr;
    },
    fullNameFn(){
        return this.firstName + " "+ this.lastName;
    }
  },
  watch:{
    firstName:function(value){
      this.fullName=value +" " +this.lastName;
    },
    lastName:function(value){
      this.fullName=this.firstName+" "+value;
    }
      
    }
  
 
}
</script>

<style>

</style>