## 为什么我们需要按需加载

## 实现按需加载用到的基础知识

### webpack提供的require.ensure函数

从执行方面，require.ensure(dependencies,callback,chunkName)函数的作用是在需要的时候才去下载所依赖的模块，当所依赖的模块下载完毕之后(下载的模块未执行)，便去执行回调函数。

从分割文件方面，require.ensure()函数会创建一个chunk，如果一个chunk的名称已经存在了，那么本次所指定依赖的模块将合并到已经存在的chunk中去，最后在webpack构建项目时会单独生成一个文件。

下面介绍一下require.ensure()函数的参数

**参数1：**dependencies 依赖模块的数组

**参数2：**callback 回调函数，该函数调用时会传一个require参数

**参数3：**chunkName 模块名，用于构建时生成文件时命名使用

#### 注意点

require.ensure()的模块只会被下载下来，不会被执行，只有在callback函数中使用require(模块名)后，这个模块才会被执行。

## 配合React-router实现按需加载

平时我们在写router时，对应的组件在component中指定，为了实现动态去加载组件，我们将component属性改为getComponent，这个属性是react-router为按需加载提供的方案。

在路由文件中，我们首先将每个页面依赖的模块使用require.ensure()函数打包成独立chunk，然后在react-router的router中指定getComponet

```javascript
const home = (location, callback) => {
  require.ensure([], require => {
    callback(null, require('modules/home'))
  }, 'home')  
}

const blog = (location, callback) => {
  require.ensure([], require => {
    callback(null, require('modules/blog'))
  }, 'blog')  
}

<Router history={history}>
  <Route path="/" component={App}>
    <Route path="home" getComponent={home}></Route>
    <Route path="blog" getComponent={blog}></Route>
  </Route>
</Router>
```

