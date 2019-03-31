
<template>
  <div id="app">

  <input type="number" name="num1" v-model="num1">
  <input type="number" name="num2" v-model="num2">
  <button @click="add">+</button>
  <button @click="subtract">-</button>
  <button @click="product">*</button>
  <button @click="divide">/</button>
  <div id="result">{{result}}</div>
  </div>
</template>

<script>
export default {
  name : "app",
  data() {
    return {
      result : '',
      num1:0,
      num2:0
    };
  },
  methods:{
    add : function(){
      this.result = parseInt(this.num1) + parseInt(this.num2)
      this.num1 = this.result
      this.num2 = 0
    },
    subtract : function(){
      this.result = parseInt(this.num1) - parseInt(this.num2)
      this.num1 = this.result
      this.num2 = 0

    },
    product : function(){
      this.result = parseInt(this.num1) * parseInt(this.num2)
      this.num1 = this.result
      this.num2 = 0
      
    },
    divide : function(){
      this.result = parseInt(this.num1) / parseInt(this.num2)

    }
  }
};
</script>

<style>
#app {
  font-size: 18px;
  font-family: 'Roboto', sans-serif;
  color: blue;
}
</style>