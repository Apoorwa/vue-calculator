
<template>
  <div id="app">
  <input type="number" name="num1" v-model="num1"/>
  <br><br>
  <div>
  <button class="button" @click="clear">AC</button>
  <button class="button"  >+/-</button>
  <button class="button" >%</button>
  <button class="button"  @click="setOperator('divide')">/</button>
  <br><br>
  <button class="button"  @click="setValue(9)">9</button>
  <button class="button"  @click="setValue(8)">8</button>
  <button class="button"  @click="setValue(7)">7</button>
  <button class="button"  @click="setOperator('product')">*</button>
  <br><br>
  <button @click="setValue(6)">6</button>
  <button @click="setValue(5)">5</button>
  <button @click="setValue(4)">4</button>
  <button @click="setOperator('subtract')">-</button>
  <br><br>
  <button @click="setValue(3)">3</button>
  <button @click="setValue(2)">2</button>
  <button @click="setValue(1)">1</button>
  <button @click="setOperator('add')">+</button>
  <br><br>
  <button @click="setValue(0)">0</button>
  <button @click="setValue(1)">.</button>
  <button @click="equals">=</button>
  <!-- <div id="result">{{result}}</div> -->
  </div>
  </div>
</template>

<script>
export default {
  name : "app",
  data() {
    return {
      result : [],
      num1:0,
      num2:0,
      operator : ''
    };
  },
  methods:{
    setOperator : function(val){
      this.operator = val      
      if(this.isOperator(this.result[this.result.length-1])){
        this.result.pop();
        this.result.push(val)
      }
      else if (this.result.length === 1){
          this.result.push(val)
        }
      else{
        let x1 = this.result.pop()
        let operator = this.result.pop()
        let x2 = this.result.pop()
        let res = this.calculate(x1,x2,operator)
        this.result.push(res)
        this.result.push(val)
      }
    },
    calculate : function(x1,x2,operator){
      let output = 0
      switch (operator){
        case 'add' : 
          output = x1 + x2
          this.num1 = output
          break
        case 'subtract' :
          output = x2 - x1
          this.num1 = output
          break
        case 'product' : 
          output = x2 * x1
          this.num1 = output
          break
        case 'divide' : 
          output = x2 / x1
          this.num1 = output
          break
        default : 
          this.num1 = output


      } 
      return output
    },
    equals: function(){
      this.setOperator(this.operator)
      // this.calculate(this.num2,this.num1,this.operator)
    },
    isOperator : function(val){
      if(val === 'add' ||
         val === 'subtract' ||
         val === 'divide' ||
         val === 'product'){
           return true
         }
    },
    setValue : function(val){
      let item = this.result.pop()
      this.result.push(item)
      if(this.isOperator(item)){    
        this.num1 =  val
        this.num2 = val
        this.result.push(this.num1)
      }
      else{
      this.num1 = parseInt(this.num1.toString() + val.toString())
        this.result.pop()
        this.result.push(this.num1)
        this.num2 = this.num1
      }
    },
    clear : function(){
      this.result  = []
      this.num1 = 0
      this.num2 = 0
      this.operator = ''
    }
  }
};
</script>

<style>
#app {
  font-size: 18px;
  font-family: 'Roboto', sans-serif;
  color: blue;
  border-style: ridge;
  /* max-width: fit-content; */
  width: 400px;
  height: 300px;
  background-color: grey;
  margin-left: 30%;
  margin-top: 20%;
}
button {
  height: 30px;
  width: 90px;
}
input {
  height: 25px;
  width: -webkit-fill-available
}
</style>