前前后后做了好几个基于React技术栈的项目，每次在一个项目刚开始架构的时候，都需要考虑如何去设计软件结构和组成，需要考虑哪些方面的问题，用哪些模块和工具去解决这些问题比较合适，即便做了几个项目之后，每次新项目还是会忽略掉一些问题，导致在开发过程中不方便，或者是需要对软件结构修修补补。

<!--more-->

现在结合自己的经验做一些梳理，把基于React技术栈去架构一个项目时，多数情况下需要考虑的问题和一些解决思路整理出来，一方面希望做一些自己的总结，另一方面希望为刚开始设计React项目结构的小伙伴提供一些参考。

我认为一个React技术栈项目，应该考虑以下问题：

## 模块化打包工具
目前一般react项目配合使用的打包工具为webpack，这是最基础的，通过npm把webpack安装到项目里，然后在项目中新建webpack.config.js文件，在该文件中配置webpack就可以了

## 实现本地开发环境
方便好用的本地开发环境能够提升开发效率和开发体验，比较推荐webpack官方推出的webpack-dev-server，这是一个小型的express服务器，主要特性是支持热加载。

## 转码器

为了提高开发效率和体验，我们会使用一些自己喜欢的语法和框架去开发，但浏览器未必能够解析这些语法，这是就需要用到babel，babel是一个全家桶式的转码器，几乎可以满足我们所有的转码需求，对于一般项目有来说，我们需要转码react以及es6的语法，某些项目中还需要用到es7的语法，也可以使用babel来转码。

babel的基本使用方式很简单，在项目中安装需要的npm模块，然后在项目根目录一下写入配置文件.babelrc即可，常用模块如有

```bash
# ES2015转码规则
$ npm install --save-dev babel-preset-es2015

# react转码规则
$ npm install --save-dev babel-preset-react

# ES7不同阶段语法提案的转码规则（共有4个阶段），选装一个
$ npm install --save-dev babel-preset-stage-0
$ npm install --save-dev babel-preset-stage-1
$ npm install --save-dev babel-preset-stage-2
$ npm install --save-dev babel-preset-stage-3
```

然后在项目根目录下的配置文件中加入这些规则，babel的配置文件为.babelrc

```javascript
{
    "presets": [
      "es2015",
      "react",
      "stage-2"
    ],
    "plugins": []
  }
```

需要注意的是，babel默认只转新的JavaScript句法而不会转新的API，比如Iterator、Generator、Set、Maps、Proxy、Reflect、Symbol、Promise等全局对象，以及一些定义在全局对象上的方法（比如`Object.assign`）都不会转码。如果需要转这些API，需要用到babel-polyfill

安装命令

```bash
npm i --save babel-polyfill
```

然后在头部引入

```javascript
import 'babel-polyfill';
// 或者
require('babel-polyfill');
```

## 配置webpack的loaders

对于一个react+webpack项目来说，配置loaders是必须的，首先需要理解一下什么是loaders，这里我们可以把loaders理解成webpack的一个中间件。由于webpack本身只能打包符合commonjs规范的js文件，所以在项目开发过程中我们需要用到的其他文件是无法被webpack打包的，比如css文件/JSX文件等，而loaders这个中间件的作用就是在webpack打包前，将原本无法被webpack打包的文件编译成符合规范js的文件，这样一来在项目中无论我们需要用到什么样的文件，只要为这些文件指定其对应的loader就可以了。

## CSS解决方案

在项目中css是很重要的部分，