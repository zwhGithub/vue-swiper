<template>
    <section class="wh_content" @touchmove="fn">
        <div id="wh_swiper" @touchstart="s" @touchmove="m" @touchend="e">
            <slot/>
        </div>

        <div v-if="showIndicator" class="wh_indicator">
            <div v-for="(tag,$index) in slidesLength" v-bind:class="{ wh_show_bgcolor: index-1==$index }" class="wh_indicator_item"></div>
        </div>
    </section>
</template>

<script>
export default {
  data() {
    return {
      slidesLength: 1,
      _width: 0,
      auto: true,
      slideing: true,
      timer1: '',
      dom: {},
      t: {
        sx: 0,
        s: 0,
        m: 0,
        e: 0
      },
      index: 1
    };
  },
  props: {
    //滑动所需要的时间
    autoPlay: {
      default: true
    },
    //一次滑动需要走多久
    duration: {
      default: 500
    },
    //两次滑动间隔的时间
    interval: {
      default: 2500
    },
    showIndicator: {
      default: true
    }
  },
  mounted() {
    //克隆dom
    this.starDom();
    this.dom.transform = `translate3d(${this._width * -1}px, 0px, 0px)`;
    if (this.autoPlay) {
      this.setTime();
    }
  },
  methods: {
    s(x) {
      if (this.slideing) {
        this.auto = false;
        window.clearTimeout(this.timer1);
        this.t.sx = this.getTransform();
        this.t.s = x.touches[x.touches.length - 1].clientX;
      }
    },
    m(x) {
      if (this.slideing && this.t.s != -1) {
        this.auto = false;
        window.clearTimeout(this.timer1);
        this.dom = this.dom;
        this.t.m = x.touches[x.touches.length - 1].clientX - this.t.s;
        this.setTransform(this.t.m + this.t.sx);
      }
    },
    e(x) {
      if (this.slideing && this.t.s != -1) {
        this.auto = false;
        window.clearTimeout(this.timer1);
        this.setTransform(this.t.m + this.t.sx);
        var x = this.getTransform();
        console.log(x);
        x += this.t.m > 0 ? this._width * 0.3 : this._width * -0.3;
        console.log(x);
        this.index = Math.round(x / this._width) * -1;
        this.wh('touch');
      }
    },
    setTransform(num) {
      this.dom.transform = `translate3d(${num}px, 0px, 0px)`;
    },
    getTransform() {
      var x = this.dom.transform;
      x = x.substring(12);
      x = x.match(/(\S*)px/)[1];
      return Number(x);
    },
    fn(e) {
      e.preventDefault();
    },
    wh(type) {
      this.slideing = false;
      this.dom.transition = type == 'touch' ? '250ms' : this.duration + 'ms';
      this.setTransform(this.index * -1 * this._width);
      this.t.m = 0;
      this.t.s = -1; //保证下次重新赋值
      if (this.autoPlay) {
        this.setTime();
      }
      var timeDuration = type == 'touch' ? '250' : this.duration;
      setTimeout(() => {
        this.dom.transition = '0s';
        if (this.index >= this.slidesLength + 1) {
          this.index = 1;
          this.setTransform(this.index * -1 * this._width);
        }
        if (this.index <= 0) {
          this.index = this.slidesLength;
          this.setTransform(this.index * -1 * this._width);
        }
        this.$emit('transtionend', this.index - 1);
        this.auto = true;
        this.slideing = true;
      }, timeDuration);
    },
    setTime() {
      this.timer1 = window.setTimeout(() => {
        if (this.auto) {
          this.index++;
          this.wh();
        } else {
          window.clearTimeout(this.timer1);
        }
      }, this.interval);
    },
    starDom() {
      var SlideDom = document.getElementsByClassName('wh_slide');
      this.slidesLength = SlideDom.length;
      var cloneDom1 = SlideDom[0].cloneNode(true); //向最后append
      var cloneDom2 = SlideDom[this.slidesLength - 1].cloneNode(true); //向最前append
      document.getElementById('wh_swiper').insertBefore(cloneDom2, SlideDom[0]);
      document.getElementById('wh_swiper').appendChild(cloneDom1);
      this._width = window.screen.availWidth;
      this.dom = document.getElementById('wh_swiper').style;
    }
  }
};
</script>

<style>
.wh_content {
  position: relative;
  z-index: 1;
  overflow: hidden;
  width: 100%;
}
#wh_swiper {
  width: 100%;
  display: -webkit-box;
  display: -ms-flexbox;
  transition-duration: 0s linear;
}
.wh_indicator {
  position: absolute;
  bottom: 8px;
  width: 100%;
  text-align: center;
  background: 0 0;
}
.wh_indicator_item {
  display: inline-block;
  width: 8px;
  height: 8px;
  margin: 1px 7px;
  cursor: pointer;
  border-radius: 100%;
  background: #aaa;
}
.wh_show_bgcolor {
  background: #0fc37c;
}
</style>
