<template>
  <div class="hello">
    <Swiper v-if="list.length>0">
      <Slide v-for="(tag,key) in list" :key=key>
        <img :src=tag />
      </Slide>
    </Swiper>
  </div>
</template>

<script>
// import { Swiper, Slide } from 'vue-swiper-component';
import { Swiper, Slide } from './index.js';
// import Swiper from './swiper';
// import Slide from './slide';
export default {
    data() {
        return {
            list: [
                'https://qiniu.epipe.cn/5456575529551388672?imageslim&imageView2/1/w/750/h/360',
                'https://qiniu.epipe.cn/5430983074181545984?imageslim&imageView2/1/w/750/h/360',
                'https://qiniu.epipe.cn/5464226412548325376?imageslim&imageView2/1/w/750/h/360'
            ]
        };
    },
    components: {
        Swiper,
        Slide
    }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
img {
    width: 100%;
}
</style>
