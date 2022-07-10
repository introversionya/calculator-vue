<template>
  <div class="calc" v-cloak>
    <div class="calc__res">{{ defaultResult }}</div>
    <div class="calc__btns">
      <Button @click="clickedNumber(7)">7</Button>
      <Button @click="clickedNumber(8)">8</Button>
      <Button @click="clickedNumber(9)">9</Button>
      <Button @click="clickedNumber('/')">/</Button>
      <Button @click="delLastChar">DEL</Button>
      <Button @click="clickedNumber(4)">4</Button>
      <Button @click="clickedNumber(5)">5</Button>
      <Button @click="clickedNumber(6)">6</Button>
      <!-- <Button @click="clickedOperation('*')">*</Button> -->
      <Button @click="clear">C</Button>
      <Button @click="clickedNumber(1)">1</Button>
      <Button @click="clickedNumber(2)">2</Button>
      <Button @click="clickedNumber(3)">3</Button>
      <!-- <Button @click="test">-</Button> -->
      <!-- <Button @click="test">(</Button> -->
      <Button @click="clickedNumber(0)">0</Button>
      <!-- <Button @click="test">.</Button> -->
      <!-- <Button @click="calc('=')">=</Button> -->
      <Button @click="clickedNumber('+')">+</Button>
      <!-- <Button @click="test">)</Button> -->
    </div>
  </div>
</template>

<script>

import Button from "@/components/Button";

export default {
  components: {
    Button,
  },

  data() {
    return {
      defaultResult: "0",
      a: "",
      b: "",
      operator: "",
      collectionOperators: ["+", "-", "/", "*"],
      // example: ""
    };
  },
  methods: {
    // Ввод чисел
    clickedNumber(number) {
      // При вводе удаляем "0"
      if (this.defaultResult.length >= 1 && this.defaultResult === "0") {
        this.defaultResult = "";
      }

      this.defaultResult += number;

      // this.a += number; // Заполняем "a" - первый числовой аргумент
      // this.example = this.a + this.b; // Заполняем "example" - конечный пример
      // Если введен оператор, то заполняем "b"
      // this.defaultResult = this.example; // Вывод примера
    },
    // Сброс ввода
    clear() {
      this.defaultResult = "";
    },
    // Удаление последнего символа
    delLastChar() {
      this.defaultResult = this.defaultResult.slice(0, -1);
    },
    // Посчитать при нажатии "="
    calc() {
      // console.log("this.a: ", this.a);
      // console.log("operator:", this.operator);
    },
    // Проверка на ввод оператора
    isLastCharOperator() {
      if (this.collectionOperators.includes(this.defaultResult.slice(-1))) return this.operator = this.defaultResult.slice(-1);
    },
    // Проверка на двойной ввод оператора
    checkDoubleOperator() {

      // let tmp = this.example.slice(-2).split(""); // 2 последних числа в массиве
      // if (tmp.length === 2) {
      //   if (this.collectionOperators.includes(tmp[0]) && this.collectionOperators.includes(tmp[1])) {
      //     this.example = this.example.slice(0, -1);
      //     // console.log("два оператора");
      //     console.log(this.example);
      //   }
      // }
    },
    // При пустом вводе добавляем "0"
    isResultEmpty() {
      if (this.defaultResult === "") return this.defaultResult = "0";
    }
  },
  watch: {
    defaultResult: function() {
      this.isResultEmpty();
      this.isLastCharOperator();
      this.checkDoubleOperator();
      this.calc();
    }
  },
};
</script>

<style lang="scss">
* {
  margin: 0;
  box-sizing: border-box;
  image-rendering: -webkit-optimize-contrast;
}

[v-cloak] {
  display: none;
}

body {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100vh;
  padding: 22px;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  background-color: #636363;
}

button {
  font-family: inherit;
  padding: 0;
}

.calc {
  width: 100%;
  max-width: 450px;
  height: 100%;
  max-height: 300px;
  border: 2px solid #bab6d4;
  border-radius: 5px;
  display: flex;
  flex-direction: column;
  background-color: #2d2d2d;
  &__res {
    font-size: 40px;
    padding: 0 5px;
    background-color: #bab6d4;
    border-bottom: 1px solid #000000;
    text-align: right;
    overflow-y: hidden;
    overflow-x: scroll;
    scrollbar-width: none;
    &::-webkit-scrollbar {
      width: 0;
      height: 0;
    }
  }
  &__btns {
    width: 100%;
    height: 100%;
    display: flex;
    flex-wrap: wrap;
    user-select: none;
  }
}
</style>
