<template>
<!-- 
  <input type="number" v-model="input[0]"><input type="checkbox" @click="()=>{select(0)}" /><br>
  <input type="number" v-model="input[1]"><input type="checkbox" @click="()=>{select(1)}" /><br>
  <input type="number" v-model="input[2]"><input type="checkbox" @click="()=>{select(2)}" /><br> -->
  <div v-for="(data, index) in checked" :key="index">
    <input type="number" v-model="input[index]" @input="changeInput($event, index)">
    <input type="checkbox" v-model="checked[index]" @change="changeCheck($event, index)"> 
  </div>
  <br>
  <button @click="operate('+')">+</button>
  <button @click="operate('-')">-</button>
  <button @click="operate('x')">x</button>
  <button @click="operate('/')">/</button>
  <h1>{{ result }}</h1>
  <h1>{{ checked }}</h1>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
// import _ from 'lodash'

export default {
  name: 'App',
  data() {
    return {
      checked: [false, false, false],
      input: [],
      result: 0
    }
  },
  methods: {
    operate(op) {
      this.result = 0;
      const isValid = this.checked.filter(value => value == true);
      if(isValid.length <= 1) {
        alert("Silahkan Pilih Checkbox");
      }
      else {
        if(op == '+') {
          this.checked.forEach((item, index) => {
            if(item) {
              this.result += parseInt(this.input[index]);
            }
          })
        } else if(op == '-') {
          this.checked.forEach((item, index) => {
            if(item) {
              if(this.result == 0) {
                this.result += parseInt(this.input[index])
              } else {
                this.result -= parseInt(this.input[index]);
              } 
            }
          });
        } else if(op == 'x') {
          this.checked.forEach((item, index) => {
            if(item) {
              if(this.result == 0) {
                this.result += parseInt(this.input[index])
              } else {
                this.result *= parseInt(this.input[index]);
              } 
            }
          });
        } else if(op == '/') {
          this.checked.forEach((item, index) => {
            if(item) {
              if(this.result == 0) {
                this.result += parseInt(this.input[index])
              } else {
                this.result /= parseInt(this.input[index]);
              } 
            }
          });
        }
      }
    },
    changeCheck(event, index) {
      // clear input unchecked
      if (!event.target.checked) {
        this.input[index] = '';
      }
    },
    changeInput(event, index) {
      if(event.target.value) {
        this.checked[index] = true;
      }else {
        this.checked[index] = false;
      }
    }
  }
}
</script>

<style scoped>
  input {
    margin-top: 8px;
  }

  button {
    margin-right: 8px;
  }

</style>
