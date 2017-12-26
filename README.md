## vue-swiper
- 基于Vue2.0开发，基本满足大部分功能
- 轻量、高性能轮播插件。目前支持  无缝衔接自动轮播、无限轮播、手势轮播


## Install

```
npm i vue-swiper-component --save
cnpm i vue-swiper-component --save  //国内镜像
```

## demo

 ![效果](https://zwhgithub.github.io/vue-swiper/dist/1514291260.png)

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
  <Swiper v-if="slidesReal.length > 0"
  		  :autoPlay='true' //是否自动轮播
          @transtionend='move' //每次轮播之后调用的方法，参数是跳到第几个轮播图
  		  :showIndicator='true' //是否显示轮播的那个点
  		  interval="2500" //每两次隔多久滚动一次
  		  duration="500"  //每次滚动一页需要多久时间
  		  >
        <Slide @click="clickMe" v-for="(tag,key) in slidesReal" :key="key">
        	//添加click事件
        </Slide>
   </Swiper>

```

## API

| 属性            | 说明           | 默认   |
| ------------- | ------------ | ---- |
| autoPlay      | 是否自动轮播       | true |
| showIndicator | 是否显示轮播的那个点   | true |
| interval      | 每两次隔多久滚动一次   | 2500 |
| duration      | 每次滚动一页需要多久时间 | 500  |

## 事件

```
transitionend 事件  每次轮播出发 参数表示轮播到第几个图片
click  事件 每个轮播图上的事件
```

## Other

- 可以通过覆盖我的样式进行自定义样式，Slide标签里面可以写div或者其他的东西
- 一些参数配置可以参考上面Usage 第三个示例，异步渲染要加v-if 保证渲染成功 参考第一个示例
- 如果其他问题可以邮箱沟通，452216418@qq.com;