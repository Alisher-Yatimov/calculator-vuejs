<template>
  <div class="calculator">
    <div class="result">{{current || 0}}</div>
    <div class="btn del" @click="del">C</div>
    <div class="btn oper" @click="split">/</div>
    <div class="btn" @click='entreNum("7")'>7</div>
    <div class="btn" @click='entreNum("8")'>8</div>
    <div class="btn" @click='entreNum("9")'>9</div>
    <div class="btn oper" @click="mult">x</div>
    <div class="btn" @click='entreNum("4")'>4</div>
    <div class="btn" @click='entreNum("5")'>5</div>
    <div class="btn" @click='entreNum("6")'>6</div>
    <div class="btn oper" @click="minus">-</div>
    <div class="btn" @click='entreNum("1")'>1</div>
    <div class="btn" @click='entreNum("2")'>2</div>
    <div class="btn" @click='entreNum("3")'>3</div>
    <div class="btn oper" @click="plus">+</div>
    <div class="btn zero" @click='entreNum("0")'>0</div>
    <div class="btn" @click="dot">.</div>
    <div class="btn oper equal" @click="equal">=</div>

  </div>
</template>

<script>
export default{
  data(){
    return{
      current: '',
      previous: null,
      operator: null,
      operatorClicked: false
    }
  },
  methods: {
    del(){
      this.current = '';
    },
    entreNum(number){
      if(this.operatorClicked){
        this.current = '';
        this.operatorClicked = false;
      }
      this.current += number;
    },
    setPrevious(){
      this.previous = this.current;
      this.operatorClicked = true;
    },
    split(){
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    mult(){
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    plus(){
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    minus(){
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    dot(){
      if(this.current.indexOf('.') === -1){
      this.entreNum('.');
      }
    },
    equal(){
      this.current = `${this.operator(parseFloat(this.current), parseFloat(this.previous))}`
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .calculator{
    display: grid;
    border: black;
    border-radius: 25px;
    border: #55CC77;
    grid-template-columns: repeat(4, 1fr);
    grid-template-rows: 120px repeat(5, 75px);
    grid-gap: 3px;
    font-size: 25px;
  }
  .del{
    grid-column: 1/4;
  }
  .zero{
    grid-column: 1/3;
    border-bottom-left-radius: 25px;
  }
  .result{
    grid-column: 1/-1;
    background: #fff;
    border-top-left-radius: 25px;
    border-top-right-radius: 25px;
  }
  .btn{
    background: #C0F8B3;
    text-align: center;
    vertical-align: middle;
  }
  .oper{
    background: #F7BD66;
  }
  .equal{
    border-bottom-right-radius: 25px;
  }

</style>
