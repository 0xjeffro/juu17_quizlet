<template>
  <div style="border-radius:16px; background-color: white;
  padding: 20px 30px; margin: 0 15px;">
    <van-row justify="center">
      <van-rate
          v-model="value"
          :size="32"
          color="#ffd21e"
          void-icon="star"
          void-color="#eee"
          :count="3"
          readonly
      />
    </van-row>
    <van-row justify="center" style="margin-top: 14px">
      <span style="font-size: larger; font-weight: bolder">{{value}}/3</span>
    </van-row>
    <van-row justify="center" style="margin-top: 5px">
      <van-image
          width="140"
          height="140"
          :src="require(`../assets/success.png`)"
          v-if="value === 3"
      />
      <van-image
          width="140"
          height="130"
          :src="require(`../assets/falling.png`)"
          v-if="value !== 3"
      />
    </van-row>


  </div>
</template>

<script>
import {Rate} from 'vant';
import { Row } from 'vant';
import { Image as VanImage } from 'vant';
import { Loading } from 'vant';
export default {
  name: "ResultCard",
  props: {
    score: Number,
  },
  data() {
    return {
    };
  },
  components: {
    [Rate.name]: Rate,
    [Row.name]: Row,
    [VanImage.name]: VanImage,
    [Loading.name]: Loading
  },
  computed: {
    value: {
      get() {
        console.log('score', this.score)
        return this.score
      },
      set(newValue) {
        // read only, so do nothing
        console.log(newValue)
      },
    }
  },
}
</script>

<style scoped>

</style>
