### 前端开发：
模块化（js的模块化、css的模块化、资源的模块化）
组件化（复用先有的UI结构、样式、行为）
规范化（目录结构的划分、编码规范化、接口规范化、文档规范化）
自动化（自动化构建、自动部署、自动化测试）
### 前端工程化
在企业级的前端项目开发中，把前端开发所需的工具，技术，流程，经验等进行规范化、标准化

好处：
前端开发自成体系，有一套标准的开发方案和流程

### 前端工程化的解决方案
早期：grunt gulp
目前主流的：webpack parcel 


### 什么是webpack
概念：webpack是前端项目工程化的具体解决方案
主要功能：它提供了友好的前端模块化开发支持，以及代码压缩混淆，处理浏览器端JavaScript的兼容性、性能优化等强大的功能
好处：让程序员把工作的重心放在具体功能的实现上，提高了前端的开发效率和项目的可维护性
（目前Vue,React等前端项目，基本上都是基于webpack进行工程化开发的）

### webpack笔记
npm i jquery -S
npm i webpack@5.42.1 webpack-cli@4.7.2 -D

-S 是--save的简写 存于dependencies 表示开发，上线部署都会用到的包
-D 是--save-dev的简写 存于devDependencies  表示只在开发阶段用到，上线之后就不用了

要不要带-D -S去看npmjs.com查看该配置项是否携带该参数

安装完后要进行配置

结论：开发时候一定要用development，因为追求的是打包的速度，而不是体积
反过来，发布上线的时候一定要用production，因为上线追求的是体积小，而不是速度

1、webpack默认只能打包js结尾的文件，处理不了其他后缀的文件
2、由于代码中包含index.css的文件，因此webpack默认处理不了
3、当webpack发现某个文件处理不了的时候，会查找webpack.config.js这个配置文件，看module.rules数组中，是否配置了对应的loader加载器
4、webpack把index.css这个文件，先转交给最后一个loader进行处理（西安转交给css-loader)
5、当css-loader处理完毕之后，会把处理的结果，转交给下一个loader（转交给style-loader)
6、当style-loader处理完毕之后，发现没有下一个loader了，于是就把处理的结果，转交给了webpack
7、webpack是style-loader处理的结果，合并到/dist/main.js中，最终生成打包好的文件


### Vue的两个特性：
1、数据驱动视图
数据的变化会驱动视图自动更新
好处：程序员只管把数据维护好，那么页面结构会被vue自动渲染出来！
2、双向数据绑定
form表单采集数据，ajax提交数据
好处：开发者不再需要手动操作DOM元素，来获取表单元素最新的值！
js数据的变化，会被自动渲染到页面上
页面上表单采集的数据发生变化的时候，会被vue自动获取到，并更新到js数据中
### MVVM
MVVM是vue实现数据驱动视图和双向数据绑定的核心原理，MVVM指的是Model,View,和ViewModel,它把每个HTML页面拆分了这三个部分
Model:表示当前页面渲染时所依赖的数据源。
View：表示当前页面所渲染的DOM结构
ViewModel：表示vue的实例，它是MVVM的核心

注意：数据驱动视图和双向数据绑定的底层原理是MVVM

### vue组件的三个组成部分
每个.vue组件都由3部分构成，分别是：
template :组件的模板结构
script : 组件的JavaScript行为
style :组件的样式
其中template是每个组件都必须包含的模板结构，而script行为和style样式是可选的组成部分

### 组件化
组件在被封装之后，彼此之间是相互独立的，不存在父子关系
在使用组件的时候，根据彼此的嵌套关系，形成了父子关系，兄弟关系

使用组件的三个步骤：
步骤一：使用Import语法导入需要的组件
import Left from '@/components/Left.vue'
步骤二：使用components结点注册组件
export default{
    components:{
        Left
    }
}
步骤三：以标签形式使用刚才注册的组件
<Left></Left>




