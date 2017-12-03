---
title: react中的无状态组件与高阶组件
categories: JavaScript
作者: 信达
date: 2017-12-03 23:45:46
tags: 
- react
---

react组件我们非常熟悉，平时开发过程中一直使用，在react开发过程中，有两种比较特殊的组件，分别为无状态组件和高阶组件，今天一起来理解一下他们。

<!--more-->

### 无状态组件

无状态组件是从react 0.14版本开始出现的，他可以用来创建纯展示型的组件，这种组件只负责根据传入的props进行展示，下面是它的基本形式：

```jsx
function HelloComponent(props){
    return (
    	<div>{props.name}</div>
    )
}

ReactDOM.render(<HelloComponent name='xinda' />,element)
```

无状态组件的一些特点如下

- 组件不会被实例化，被精简成了render()方法的一个函数来实现的，从而性能能够有所提升。
- 组件不能访问this对象，无状态组件由于没有实例化过程，因此无法访问this中的对象。
- 组件没有声明周期的方法。
- 无状态组件只能访问输入的props，同样的props会得到同样的渲染结果，不会有副作用。

无状态组件有着良好的阅读型，是用来分割复杂组件的利器，所以只要有可能，应该尽量使用无状态组件。

### 高阶组件

高阶组件就是一个没有副作用的纯函数，它接受一个组件，返回一个新组件。

假设有如下两个组件：

##### 组件1：welcome组件

```jsx
import React, {Component} from 'react';

class Welcome extends Component {
  constructor(props){
    super(props);
    this.state = {
      username : ''
    }
  }
  
  componentWillMount(){
    let username = localStorage.getItem('username');
    this.setState({
      username:username
    })
  }
  
  render(){
    return (
    	<div>Welcome , {this.state.username}</div>
    )
  }
  
}
```

##### 组件2：goodbey组件

```jsx
import React, {Component} from 'react';

class Goodbey extends Component {
  constructor(props){
    super(props);
    this.state = {
      username : ''
    }
  }
  
  componentWillMount(){
    let username = localStorage.getItem('username');
    this.setState({
      username:username
    })
  }
  
  render(){
    return (
    	<div>Goodbey , {this.state.username}</div>
    )
  }
  
}
```

可以看到，上面的两个组件中从localStorage获取username，再将username保存到state中，这两个步骤代码是重复的，既会造成代码的冗余，也会造成在调整username时需要对两个组件的代码进行修改，因此我们需要一种方法，能够抽取这部分代码，让组件更加简洁和易于维护，高阶组件可以解决这个问题，示例代码如下：

##### 高阶组件

```jsx
export default (wrapComponent) => {
  class NewComponent extends Component{
    constructor(){
      super();
      this.state = {
        username : ''
      }
    }
    componentWillMount(){
      let username = localStorage.getItem('username');
      this.setState({
        username:username
      })
    }
    render(){
      return <wrapComponent username={this.state.username} />
    }
    
  }
  return NewComponent;
}
```

高阶组件就是一个函数，他从参数wrapComponent接收了一个组件，并生成了一个新的组件，新组件通过内部逻辑将username作为props传递给了传入组件，并将组件返回，有了这个高阶组件后，之前的welcome组件和goodbey组件就可以简化了

##### welcome组件

```jsx
import React , {Component} from 'react';
import wrapWithUsername from 'wrapWithUsername';

class Welcome from Component {
  render(){
    return (
    	<div>welcome,{this.props.username}</div>
    )
  }
}

Welcome = wrapWithUsername(Welcome);
export default Welcome;

```

##### goodbey组件

```jsx
import React , {Component} from 'react';
import wrapWithUsername from 'wrapWithUsername';

class Goodbey extends Component {
  render(){
    return (
    	<div>goodbey,{this.props.username}</div>
    )
  }
}
Goodbey = wrapWithUsername(Goodbey);
export default Goodbey;

```

可以看到，经过抽取高阶组件，welcome组件和goodbey组件变的非常简洁，只需要从props直接取出username使用就可以了，而不需要去管高阶组件中username的获取逻辑，如果出现username获取逻辑的修改，我们只需要修改高阶组件中的逻辑就可以了，不需要去修改使用这个组件的其他组件，维护起来也比较方便。

