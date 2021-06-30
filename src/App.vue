<template>
  <div id="app">
    <h1 class="header">Блиц-викторина</h1>
    <div class="questionWrapper" v-if="answeredQuestions.length < questionCount">
      <h3 class="question"> {{questions[currentQuestion].title}} </h3>
      <div class="answers">
       <Button v-for="(answer, index) in [...questions[currentQuestion].answers].sort(() => Math.random() - 0.5)"
               :onClickButton="onClickButton"
               :answer="answer"
               :key="index" />
      </div>
      <h6 class="info">{{`Текущий вопрос ${answeredQuestions.length + 1} из ${questionCount}`}}</h6>
    </div>
    <div class="results" v-else>
      <h3>{{ `Поздравляем! Вы ответили правильно на ${rightCount} из ${questionCount} вопросов` }}</h3>
      <button class="restartButton" v-on:click="onRestartGame">Сыграть сначала</button>
    </div>
  </div>
</template>

<script>
import '@/assets/styles/global.scss';
import Button from './components/Button';
import { questions } from '@/store';

const initialState = function () {
  return {
    currentQuestion: Math.floor(Math.random() * questions.length),
    questionCount: 10,
    rightCount: 0,
    answeredQuestions: [],
    questions
  };
};

export default {
  name: 'App',
  data: () => initialState(),
  methods: {
    onClickButton: function (isRight) {
      if (isRight) {
        this.rightCount += 1;
      }

      this.answeredQuestions.push(this.currentQuestion);

      if (this.answeredQuestions.length !== this.questionCount) {
        let rand = Math.floor(Math.random() * questions.length);
        while (this.answeredQuestions.includes(rand)) {
          rand = Math.floor(Math.random() * questions.length);
        }

        this.currentQuestion = rand;
      }
    },
    onRestartGame: function () {
      Object.assign(this.$data, initialState());
    }
  },
  components: {
    Button
  }
};
</script>

<style lang="scss">
#app {
  background-repeat: no-repeat;
  background-size: 100vw 120vh;
  display: flex;
  min-height: 100vh;
  align-items: center;
  flex-direction: column;
  font-family: "Roboto", sans-serif;
  background-image: url("https://thumbs.dreamstime.com/z/%D0%B2%D0%BE%D0%BF%D1%80%D0%BE%D1%81%D0%B8%D1%82%D0%B5%D0%BB%D1%8C%D0%BD%D1%8B%D0%B5-%D0%B7%D0%BD%D0%B0%D0%BA%D0%B8-%D1%80%D0%B0%D0%B7%D0%B1%D1%80%D0%BE%D1%81%D0%B0%D0%BD%D0%BD%D1%8B%D0%B5-%D0%BD%D0%B0-%D0%B1%D0%B5%D0%BB%D0%BE%D0%BC-%D1%84%D0%BE%D0%BD%D0%B5-%D1%82%D0%B5%D1%81%D1%82-%D1%81%D0%BE%D0%BC%D0%BD%D0%B5%D0%BD%D0%B8%D1%8F-%D0%BE%D0%BF%D1%80%D0%BE%D1%81-faq-154816321.jpg");
  .header {
    margin-top: 225px;
    font-size: 40px;
  }
  .questionWrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
    font-size: 30px;
  }
  .question {
    color: brown;
  }
  .info {
    color: blueviolet;
  }
  .answers {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: 1fr 1fr;
    grid-gap: 12px;
  }
  .restartButton {
    margin-left: 170px;
    border-radius: 50%;
    background-color: honeydew;
    color: black;
    border-color: green;
    width: 200px;
    height: 50px;
    cursor: pointer;
    &:hover {
      background-color: green;
      color: white;
    }
  }
}
</style>
