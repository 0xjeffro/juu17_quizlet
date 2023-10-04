<template>
<!--  <img alt="Vue logo" src="./assets/logo.png">-->
<!--  <HelloWorld msg="Welcome to Your Vue.js App"/>-->
  <van-config-provider :theme-vars="themeVars">
    <van-steps :active="active">
      <van-step>第一题</van-step>
      <van-step>第二题</van-step>
      <van-step>第三题</van-step>
      <van-step>完成</van-step>
    </van-steps>

    <QuestionCard v-for="(q, index) in questions" v-bind:key="index" v-show="index === active" :question="q"
                  :question-id="index + 1"
                  v-on:set-answer="setAnswer"
    />

    <result-card :score="calculateScore" v-show="active === 3"></result-card>

    <van-button
        type="primary" size="large" @click="nextQuestion"
        style="margin-top: 20px"
        :disabled="answers[active] === -1"
        v-if="active < 3"
        >
      下一题
    </van-button>

    <van-button
        :type="calculateScore === 3 ? 'success' : 'warning'" size="large"
        style="margin-top: 20px"
        :disabled="answers[active] === -1"
        v-if="active === 3"
    >
      {{calculateScore === 3 ? '恭喜通关！欢迎加入 👏' : '再接再厉'}}
    </van-button>
  </van-config-provider>
</template>

<script>
import questions from "@/questions";
import QuestionCard from './components/QuestionCard.vue'
import ResultCard from './components/ResultCard.vue'
import { reactive } from 'vue';
import { ConfigProvider } from 'vant';
import { Step, Steps } from 'vant';
import { Button } from 'vant';
import { Cell, CellGroup } from 'vant';
import 'vant/lib/index.css';

export default {
  name: 'App',
  components: {
    QuestionCard,
    ResultCard,
    [Step.name]: Step,
    [Steps.name]: Steps,
    [Button.name]: Button,
    [Cell.name]: Cell,
    [CellGroup.name]: CellGroup,
    [ConfigProvider.name]: ConfigProvider,

  },
  setup() {
    const themeVars = reactive({
      stepIconSize: '20px',
      stepCircleSize: '10px',
      stepsBackground: '#f7f7f7',
      background2: '#f7f7f7',
    })

    // 从question中随机抽取3道题目
    const randomQuestions = []
    while(randomQuestions.length < 3) {
      const index = Math.floor(Math.random() * questions.length)
      if (randomQuestions.indexOf(questions[index]) === -1) {
        randomQuestions.push(questions[index])
      }
    }
    console.log(randomQuestions)

    return {
      themeVars,
      questions: randomQuestions
    }
  },
  data() {
    return {
      active: 0,
      questionNumber: 0,
      answers: [-1, -1, -1]
    };
  },
  methods: {
    nextQuestion() {
      this.active++;
      this.questionNumber++;
    },
    setAnswer(questionId, answer) {
      console.log('set-answer', questionId, answer)
      this.answers[questionId - 1] = answer
      console.log(this.answers)
    },
  },
  computed: {
    calculateScore() {
      let score = 0
      for (let i = 0; i < this.answers.length; i++) {
        if (this.answers[i] === this.questions[i].answer) {
          score += 1
        }
      }
      return score
    }
  }

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 10px;
  margin-left: 5%;
  margin-right: 5%;
}
body {
  background-color: #f7f7f7;
}
</style>
