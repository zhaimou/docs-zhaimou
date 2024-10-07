### 为什么要进行性能优化呢
进行性能优化的原因是因为：性能的体现对干产品的影响是非常大，那么为了保证用户的留存率和转化率，我们就需要提升应用的响应速度 交互体验。以保证竞争力。
### 性能优化如何衡量
性能优化如何衡量， 也就是性能优化的标准是什么？
游览器中控制台呢有两个重要选项`Network`和`Performance`<br/>
#### Network**主要功能和指标：**
- `请求和响应时间`：显示每个网络请求的发起时间、完成时间、以及请求和响应所花费的时间（即网络延迟）。
- **文件大小**：展示每个请求的文件大小，有助于分析资源的大小是否影响了加载时间。
- **请求类型**：标明请求的类型（如文档、脚本、样式表、图像等），可以帮助识别加载哪些资源可能造成性能瓶颈。
- **HTTP 状态码**：显示服务器对请求的响应状态码（如200、404、500等），有助于诊断请求失败的问题。
- **缓存**：显示资源是否从缓存中加载（如`Cache`或`Memory Cache`），帮助了解缓存策略的效果。
- **Timeline**：提供请求的时间线视图，帮助识别资源加载的顺序和时间分布。
- **Headers**：查看请求和响应的HTTP头信息，以了解请求的具体细节和服务器的响应
 **`Network`面板**主要关注网络请求和资源加载情况，帮助优化资源大小和请求效率。<br/>
 
 **`Performance`面板**提供了详细的运行时性能数据，帮助深入分析和优化页面的加载和执行性能。
####  要衡量的重要指标
- **[首次内容绘制 (FCP)](https://web.dev/articles/fcp?hl=zh-cn)**：衡量从网页开始加载到网页内容的任何部分在屏幕上呈现的时间。_（[实验](https://web.dev/articles/user-centric-performance-metrics?utm_source=devtools&hl=zh-cn#lab)，[字段](https://web.dev/articles/user-centric-performance-metrics?utm_source=devtools&hl=zh-cn#field)）_
- **[Largest Contentful Paint (LCP)](https://web.dev/articles/lcp?hl=zh-cn)**：衡量从网页开始加载到屏幕上呈现最大的文本块或图片元素所用的时间。_（[实验](https://web.dev/articles/user-centric-performance-metrics?utm_source=devtools&hl=zh-cn#lab)，[字段](https://web.dev/articles/user-centric-performance-metrics?utm_source=devtools&hl=zh-cn#field)）_
- **[Interaction to Next Paint (INP)](https://web.dev/articles/inp?hl=zh-cn)**：衡量与网页进行的每个点按、点击或键盘互动的延迟时间，并根据互动次数选择网页最差（或接近最长的互动延迟时间）作为单个代表性值，以描述网页的整体响应能力。_（[实验](https://web.dev/articles/user-centric-performance-metrics?utm_source=devtools&hl=zh-cn#lab)，[字段](https://web.dev/articles/user-centric-performance-metrics?utm_source=devtools&hl=zh-cn#field)）_
- **[总阻塞时间 (TBT)](https://web.dev/articles/tbt?hl=zh-cn)**：衡量 FCP 和 TTI 之间的总时长，在该时间段内，主线程处于阻塞状态的时长足以阻止输入响应。_（[实验](https://web.dev/articles/user-centric-performance-metrics?utm_source=devtools&hl=zh-cn#lab)）_
- **[Cumulative Layout Shift (CLS)](https://web.dev/articles/cls?hl=zh-cn)**：衡量从网页开始加载到其[生命周期状态](https://developer.chrome.com/blog/page-lifecycle-api?hl=zh-cn)变为隐藏期间发生的所有意外布局偏移的累计得分。_（[实验](https://web.dev/articles/user-centric-performance-metrics?utm_source=devtools&hl=zh-cn#lab)，[字段](https://web.dev/articles/user-centric-performance-metrics?utm_source=devtools&hl=zh-cn#field)）_
- **[首字节时间 (TTFB)](https://web.dev/articles/ttfb?hl=zh-cn)**：衡量网络使用资源的第一个字节响应用户请求所需的时间。_（[实验](https://web.dev/articles/user-centric-performance-metrics?utm_source=devtools&hl=zh-cn#lab)，[字段](https://web.dev/articles/user-centric-performance-metrics?utm_source=devtools&hl=zh-cn#field)）_

太麻烦？看不懂可以安装`lighthouse`插件

![[Pasted image 20240912211912.png]]

![[Pasted image 20240912212002.png]]
### 项目性能优化方案
#### 数据懒加载
查看当前页面，我们可以发现：用户是没有办法一下子看完所有数据的，他需要滚动页面，才可以看到后续的数据。
那么在很多情况下就会存在这样的情况：用户可能看到第一行的商品就直接点击进入详情页面了，也就是用户可能永远都不会看到最后一行数据。那么基于这个条件，我们最后一行数据，是不是就是不需要展示的数据。那么既然是不需要展示的数据，我们是不是就应该在一开始不获取数据，等到用户将要看到它的时候，在进行数据获取和展示呢？<br/>
那么，我们就把这样一个一开始不获取数据，等到用户将要看到它的时候，再进行数据获取和展示的功能，叫做数据懒加载。<br/>
那么这样的一个数据懒加载的功能如何进行实现呢？
根据我们刚才所说，整个数据懒加载的功能一共被分为三个阶段：<br/>
1. 不获取数据
2. 用户将要看到
3. 获取数据并染
在这三个阶段中，第一和第三都比较简单，最重要的就是第二如何判断用户将要看到<br/>
那么想要实现这个目的，我们就需要利用利用到一个新的API，那就是`IntersectionObsenver`
IntersectionObserve可以`监听某一个视图是否被用户可见`<br/>
利用这`intersectionObserver`API，我们可以完成阶段二
IntersectionObserver是web的原生API，在vue3中使用没有问题，但是会略显复杂。
所以为此，vue的工具库vueuse提供了一个基于IntersectionObserver的封装方法
 uselntersectionObsenver  该方法基于IntersectionObserver完成，但是在应用层的使用中会更加方便<br/>
**相关代码实现**
```js
const box3Target = ref(null)
onMounted(() => {

// const intersectionObserver = new IntersectionObserver((entries) => {

// if (entries[0].intersectionRatio <= 0) {

// return console.log('当前视图不可见')

// }

// console.log('当前视图可见')

// })

// intersectionObserver.observe(box3Target.value)

  

const { stop } = useIntersectionObserver(

box3Target,

([{ isIntersecting }]) => {

if (isIntersecting) {

console.log('视图可见')

// 获取数据

loadData03()

// 触发 stop 监听停止

stop()

} else {

console.log('视图不可见')

}

}

)

})

```
#### 图片懒加载
和`数据懒加载`类似，咱们这里有很多的图片展示，但是用户不可能每次都看到最后的位置。那么换
而言，有很多的图片是没有必要加载的，我们只要看到图片的时候，在进行加载就可
但是：大家不要高兴的太早哦～。    
我们知道`IntersectionObserver`在每次使用的时候， 必须传入dom对象。在数据懒加载中因为我们只需要监听一个或几个指定的容器，所以可以直接使用Intersection0bserver。
但是，在图片懒加载中，img标签是非常多的，我们不可能把每个img标签的dom对象都获取到对不对。
那么怎么办呢？
此时，咱们就需要使用到自定义指令的概念了
在vue3中，我们可以通过app.directive完成自定义指令。有了指令之后，我们只要在需要图
片懒加载的img标签处，写入该指令即可
```js
import { useIntersectionObserver } from '@vueuse/core'

  

const imgLazy = {

mounted(el) {

// console.log(el)

// 图片懒加载：一开始不加载，等到将要看到时在加载

// 1. 缓存当前的图片路径

const catchSrc = el.src

console.log(catchSrc)

// 2. 把 img.src 变为占位图

el.src = 'https://res.lgdsunday.club/img-load.png'

// 3. 监听将要看到

const { stop } = useIntersectionObserver(el, ([{ isIntersecting }]) => {

if (isIntersecting) {

// 4. 渲染图片

el.src = catchSrc

// 5. 停止监听

stop()

}

K})

}

}

  

export default {

// app.use 的方式使用

install: (app) => {

app.directive('imgLazy', imgLazy)

}

}

```

#### 打包体积过大(CDN优化处理)
打包体积过大是因为第三方依赖包体积过大，而想要排除依赖包，那么需要使用`webpack`或`vite`提供的外部扩展`Extenals`属性
` 防止将某些import的包（package打包到bundle中，而是在运行时（runtime）再去从外部获取这些扩展依赖（external dependencies）`

现在，如果我们运行打包之后的项目，那么会得到一个错误可以利用 anywhere 运行打包之后的项目：
    1.安装anywhere： npm -g anywhere
    2.在dist目录下，执行终端命令: anywhere
    3.自动启动服务
这是因为我们在上一小节排除依赖，导致依赖的第三方包找不到。
那么想要解决这个问题， 我们就需要使用到另外一个功能，那就是`CDN`引入。


```js
const { defineConfig } = require('@vue/cli-service')

  

let externals = {}

let cdn = {

js: []

}

  

// 排除打包，只需要在 build 排除

const isProd = process.env.NODE_ENV === 'production'

if (isProd) {

externals = {

xlsx: 'XLSX',

echarts: 'echarts'

}

cdn = {

js: [

'https://cdn.jsdelivr.net/npm/echarts@5.4.2/dist/echarts.min.js',

'https://cdn.jsdelivr.net/npm/xlsx@0.18.5/dist/xlsx.full.min.js'

]

}

}

module.exports = defineConfig({

transpileDependencies: true,

configureWebpack: {

externals

},

chainWebpack(config) {

config.plugin('html').tap((args) => {

// 携带指定的属性到 htmlWebpackPlugin

args[0].cdn = cdn

return args

})

}

})
```
在index.html引入
```html
<!DOCTYPE html>
<html lang="">
<head>
<meta charset="utf-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="viewport" content="width=device-width,initial-scale=1.0">
<link rel="icon" href="<%= BASE_URL %>favicon.ico">
<!-- 请求不添加请求来源 -->
<meta name="referrer" content="no-referrer" />
<title>
<%= htmlWebpackPlugin.options.title %>

</title>

<style>

* {

margin: 0;

padding: 0;

}

</style>

</head>

  

<body>

<noscript>

<strong>We're sorry but <%= htmlWebpackPlugin.options.title %> doesn't work properly without JavaScript enabled.

Please enable it to continue.</strong>

</noscript>

<div id="app"></div>

<!-- built files will be auto injected -->

<!-- 引入 js -->

<% for(var js of htmlWebpackPlugin.options.cdn.js) { %>

<script src="<%=js%>"></script>

<% } %>

</body>

</html>
```
`CDN`也有自己的缺点 虽然目前项目打包体积变小了，但是用户访问项目的体积没有变小
`CDN`只能增加用户访问的速度，但是并不会减少依赖包的体积。
#### 其他优化方案

#### gzip压缩
首先咱们先说一下gzip压缩。我们在前面的打包中看到过`gzip`。
`Gzip`通过LZ77算法与Huffman编码来压缩文件，重复度越高的文件可压缩的空间就越大，对JS、CSS、HTML等文本资源均有效。
当`Nginx`返回js文件的时候，会判断是否开启gzip，然后压缩后再返回给浏览器
该压缩方法需要Nginx配置开启Gzip压缩，单纯前端通过webpack插件开启Gzip压缩是不能达到优化效果的。

#### http缓存
当我们日常刷新网页的时候，经常会遇到`304`状态码
<br/>
304状态码表示：所请求的资源未修改，服务器返回此状态码时，不会返回任何资源。客户端通常会缓存访问过的资源，通过提供一个头信息指出客户端希望只返回在指定日期之后修改的资源。<br/>
不过在大多数况下   304的处理一般在服务框架中就进行处理   前端一般不需要过于关注

#### service worker
erviceworker是一个JSAPI 它的作用是:为网站提供有效的离线体验。在这里不做过多展开 可以去mdn查看。

### 最后
本文是Sunday老师视频的笔记  [点击跳转](https://www.bilibili.com/video/BV1GAWDe7E3k/?p=16&spm_id_from=pageDriver&vd_source=e73709c9a1618b4c6dfd58c6c40d8986)<br/>

>会持续更新前端文章 如果对你有用的话就点个关注吧

