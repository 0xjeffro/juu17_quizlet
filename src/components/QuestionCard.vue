<template>
  <div style="border-radius:5%; background-color: white;
  padding: 20px 30px; margin: 0 15px;">
    <span style="color: #2c3e50; display:inline-block; font-weight: bold; font-size: small; text-align: left;">
      {{questionId}}. {{question.title}}
    </span>

    <van-button v-for="(q, index) in question.options" v-bind:key="index" plain
                :type="getButtonType(index)" block style="margin-top: 7px;" hairline
                @click="selectAnswer(index)"
    >
      {{opt[index]}}. {{q}}
    </van-button>

  </div>
</template>

<script>
import { Cell } from 'vant';
import { Button } from 'vant';
import {reactive} from "vue";
export default {
  name: 'QuestionCard',
  props: {
    questionId: Number,
    question: Object
  },
  components: {
    [Cell.name]: Cell,
    [Button.name]: Button
  },
  setup() {
    const themeVars = reactive({

    })
    return {
      themeVars
    }
  },
  data() {
    return {
      opt: ['A', 'B', 'C'],
      buttonTypes: ['default', 'primary', 'info', 'warning'],
      selected: -1
    };
  },
  methods: {
    selectAnswer(index) {
      this.selected = index
      this.$emit('set-answer', this.questionId, index)
    },
    getButtonType(index) {
      return this.selected === index ? 'primary' : 'default'
    }
  },
  computed: {
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
