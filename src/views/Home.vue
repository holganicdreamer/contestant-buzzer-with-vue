<template>
  <div @click="click">
    <div class="box">
      <img :src="imageSrc">
      <h2 v-if="displayDate">あなたの押した時刻は {{displayDate}} です。</h2>
    </div>
  </div>
</template>

<script>
import { Howl } from 'howler'
import moment from 'moment'
import RedButton from "../assets/red_button.png"
import GreenButton from "../assets/green_button.png"
import Buzzer1 from "../assets/buzzer1.mp3"
import Buzzer2 from "../assets/buzzer2.mp3"

export default {
  name: 'home',
  data: function() {
    return {
      audio: null,
      date: null,
      opt: this.$route.params.param1,
      imageSrc: null,
    }
  },
  methods: {
    click() {
      // console.log("clicked")
      this.date = moment()
      this.audio.play()
    }
  },
  computed: {
    displayDate: function() {
      if(this.date == null) {
        return null;
      }
      else {
        return this.date.format('HH:mm:ss.SS');
      }
    }
  },
  mounted () {
    if(this.$route.params.param1 == 2) {
      this.imageSrc = GreenButton
      this.audio = new Howl({ src: [Buzzer2] })
    }
    else {
      this.imageSrc = RedButton
      this.audio = new Howl({ src: [Buzzer1] })
    }
    
  },
}
</script>

<style>
.box {
  font-family: 'Lato', 'Noto Sans JP', '游ゴシック Medium', '游ゴシック体', 'Yu Gothic Medium', YuGothic, 'ヒラギノ角ゴ ProN', 'Hiragino Kaku Gothic ProN', 'メイリオ', Meiryo, 'ＭＳ Ｐゴシック', 'MS PGothic', sans-serif;
  /* background-color: pink; */
  text-align: center;
  height: 100vh;
}
.box > h2 {
  font-size: 1.5rem;
}
@media screen and (orientation: landscape) {
  .box > img {
    width: 80vh;
  }
}
@media screen and (orientation: portrait) {
  .box > img {
    width: 80vw;
  }
}
</style>
