<template>
  <button class="button" v-on:click="onClickButton(answer.isRight)">{{answer.title}}</button>
</template>

<script>
export default {
  name: 'Button',
  props: {
    answer: Object,
    onClickButton: Function
  }
};
</script>

<style scoped lang="scss">
.button {
  width: 400px;
  height: 100px;
  border-radius: 20px;
  border-color: brown;
  border-width: 3px;
  background: lavenderblush;
  font-size: 30px;
  color: crimson;
  cursor: pointer;
  &:hover {
    background-color: crimson;
    color: white;
  }
}

</style>
