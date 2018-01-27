## vue-swiper

* 基于 Vue2.0 开发，基本满足大部分功能
* 轻量、高性能轮播插件。目前支持 无缝衔接自动轮播、无限轮播、手势轮播
* 没有引入第三方库，原生 js 封装,打包之后只有 8.2KB 大小 性能还是杠杠滴

## demo

![效果](http://zwhgithub.github.io/vue-swiper/dist/1514291260.png)

* 🎉🎉🎉如果觉得好用，给一个 star 哦~~~ 🎉🎉🎉

## Install

```
npm i vue-swiper-component --save
cnpm i vue-swiper-component --save  //国内镜像
```

## Usage

```javascript
import { Swiper, Slide } from 'vue-swiper-component';

components: {
    Swiper,
    Slide
}

//异步加载轮播图的情况
  <Swiper v-if="list.length > 0">
       <Slide v-for="(tag,key) in list" :key="key">
       </Slide>
  </Swiper>


 //同步加载轮播图情况
  <Swiper>
       <Slide>
               1
       </Slide>
       <Slide>
       		2
       </Slide>
       <Slide>
       		3
       </Slide>
  </Swiper>

    //加一些参数配置情况
  <Swiper v-if="slidesReal.length > 0" :autoPlay='true' :showIndicator='true' interval="2500" duration="500">
        <Slide @click="clickMe" v-for="(tag,key) in slidesReal" :key="key">
        	//添加click事件
        </Slide>
   </Swiper>
```

## API

| 属性          | 说明                     | 默认 |
| ------------- | ------------------------ | ---- |
| autoPlay      | 是否自动轮播             | true |
| showIndicator | 是否显示轮播的那个点     | true |
| interval      | 每两次隔多久滚动一次     | 2500 |
| duration      | 每次滚动一页需要多久时间 | 500  |

```
✅  Swiper 上面还暴露了其他方法,在 Swiper 标签上添加 ref 属性, 例如: <Swiper ref="swiper"></Swiper>

    ✅  this.$refs.swiper.prevSlide(); // 上一张图
    ✅  this.$refs.swiper.nextSlide(); // 下一张图
    ✅  this.$refs.swiper.slideTo(2); //某一张图
```
## 事件

```
transitionend 事件  每次轮播出发 参数表示轮播到第几个图片
click  事件 每个轮播图上的事件
```

## Other

* 可以通过覆盖我的样式进行自定义样式，Slide 标签里面可以写 div 或者其他的东西
* 一些参数配置可以参考上面 Usage 第三个示例，异步渲染要加 v-if 保证渲染成功 参考第一个示例
* 如果其他问题可以邮箱沟通，452216418@qq.com;
