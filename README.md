# vue3实现放大镜功能

## 前置

​	作为一名前端er，爱折腾是最核心的属性，所以在这个风和日丽的下午，在上班摸鱼的路上看到了这个：[我要造轮子系列 -Vue3放大镜组件](https://juejin.cn/post/6980724800318603272)。咦，好像很厉害的鸭子。决定了，今天的这个摸鱼时光就干这个了。

<div align="center">
  <img src="https://v2fy.com/asset/0i/ChineseBQB/024Programmer_%E7%A8%8B%E5%BA%8F%E5%91%98%F0%9F%91%A8%E2%80%8D%F0%9F%92%BB%E2%80%8DBQB/%E7%A8%8B%E5%BA%8F%E5%91%9800042-%E6%88%91%E7%9A%84%E5%86%85%E5%BF%83%E9%9D%9E%E5%B8%B8Excited%E7%94%9A%E8%87%B3%E8%BF%98%E6%83%B3%E5%86%8D%E5%86%99%E4%B8%A4%E8%A1%8C%E4%BB%A3%E7%A0%81.JPG" alt="https://v2fy.com/asset/0i/ChineseBQB/024Programmer_程序员👨‍💻‍BQB/程序员00042-我的内心非常Excited甚至还想再写两行代码.JPG"/>	
</div>

## 准备
安装vue3相关环境

1. 安装npm环境（ps:可以网上搜索教程）

2. 安装Vue CLI脚手架

   ```bash
   npm install -g @vue/cli
   ```

3. 创建项目并运行

   ```bash
   npm init vite <project-name> -- --template vue
   cd <project-name>
   npm install
   npm run dev
   ```

![image-20210803144622937](./readme-images/image-20210803144622937.png)

### 踩坑1：

​	**问题描述**：在创建完项目后进入项目根目录，然后运行`npm run dev`结果就报错了

​	**报错信息**：

![image-20210803145809981](./readme-images/image-20210803145809981.png)

![https://v2fy.com/asset/0i/ChineseBQB/024Programmer_程序员👨‍💻‍BQB/程序员00034-挺秃然的.jpg](https://v2fy.com/asset/0i/ChineseBQB/024Programmer_%E7%A8%8B%E5%BA%8F%E5%91%98%F0%9F%91%A8%E2%80%8D%F0%9F%92%BB%E2%80%8DBQB/%E7%A8%8B%E5%BA%8F%E5%91%9800034-%E6%8C%BA%E7%A7%83%E7%84%B6%E7%9A%84.jpg)

**问题分析**：嗯？是按照官网操作来的啊（我一脸懵圈，难道是打开方式不对？？？），然后重新来一遍，还是报错。难道刚刚那里操作有问题，删掉node_modules，重装再来一篇。

![https://v2fy.com/asset/0i/ChineseBQB/024Programmer_程序员👨‍💻‍BQB/程序员00053-你竟然在代码里下毒.png](https://v2fy.com/asset/0i/ChineseBQB/024Programmer_%E7%A8%8B%E5%BA%8F%E5%91%98%F0%9F%91%A8%E2%80%8D%F0%9F%92%BB%E2%80%8DBQB/%E7%A8%8B%E5%BA%8F%E5%91%9800053-%E4%BD%A0%E7%AB%9F%E7%84%B6%E5%9C%A8%E4%BB%A3%E7%A0%81%E9%87%8C%E4%B8%8B%E6%AF%92.png)

**解决办法**：遇事莫慌，百度一波。咦怎么都是进错目录，然后直接进入下一级就行。（这么低级的错误是我这种牛逼的人会犯的吗？）不管了，先回去看一下，嗯，我果然没进错目录。那么再看看其他人怎么说......终于，众人之中，总有小伙伴问题跟我一致了[参考解决](https://blog.csdn.net/qq_36404808/article/details/118672341)，原来是官方问题，还提了issue，先看看怎么个情况。哦哦，跟博客说的差不多，说是应该生成`esbuild/esbuild.exe`文件的,但是不知道为什么就没有生成成功，需要手动生成一下

**结论**：在当前目录下运行`node ./node_modules/esbuild/install.js`即可

![https://v2fy.com/asset/0i/ChineseBQB/064Trump_特朗普BQB/特朗普00002-完美川普川建国.jpg](https://v2fy.com/asset/0i/ChineseBQB/064Trump_%E7%89%B9%E6%9C%97%E6%99%AEBQB/%E7%89%B9%E6%9C%97%E6%99%AE00002-%E5%AE%8C%E7%BE%8E%E5%B7%9D%E6%99%AE%E5%B7%9D%E5%BB%BA%E5%9B%BD.jpg)

