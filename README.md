# carousel

> A Vue.js project

## Build Setup

``` bash
# 安装插件
npm i vue-my-carousel

# 在main.js中引入
import MyCarousel from 'vue-my-carousel'
Vue.use(MyCarousel);

# 直接调用
<my-carousel :autoplay="true" :height="200" :interval="5000" :show-size="3" :carousel-list="dataList"></my-carousel>
```
```
参数说明：
autoplay 为true时自动播放，默认向右
height 轮播的高度
interval 轮播的时间间隔
show-size 轮播一页显示几个
carousel-list 轮播的内容
格式如下：
[
{
 url: 'https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=1519175636,579560806&fm=27&gp=0.jpg',//图片地址
 link: 'https://www.baidu.com',//后续做跳转
}
]


```
For detailed explanation on how things work, consult the [docs for vue-loader](http://vuejs.github.io/vue-loader).
