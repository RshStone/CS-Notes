# React

## [Tutorial: Intro to React – React (reactjs.org)](https://reactjs.org/tutorial/tutorial.html#what-is-react)

declarative, efficient, flexible

Components, React.Component

[react-developer-roadmap/README-CN.md at master · adam-golab/react-developer-roadmap (github.com)](https://github.com/adam-golab/react-developer-roadmap/blob/master/README-CN.md)

### Components

什么是JSX, 掌握JSX语法

组件的概念，声明组件内容和样式

如何渲染到页面

掌握简单组件划分，提取和组合

 函数组件和类组件

why 使用 JSX?

**哲学思想**

React 认为渲染逻辑本质上与其他 UI 逻辑内在耦合，比如，在 UI 中需要绑定处理事件、在某些时刻状态发生变化时需要通知到 UI，以及需要在 UI 中展示准备好的数据。

React 并没有采用将*标记与逻辑分离到不同文件*这种人为的分离方式，而是通过将二者共同存放在称之为“组件”的松散耦合单元之中，来实现[*关注点分离*](https://en.wikipedia.org/wiki/Separation_of_concerns)。

React [不强制要求](https://zh-hans.reactjs.org/docs/react-without-jsx.html)使用 JSX，但是大多数人发现，在 JavaScript 代码中将 JSX 和 UI 放在一起时，会在视觉上有辅助作用。它还可以使 React 显示更多有用的错误和警告消息。

#### JSX中嵌入表达式

```jsx
const name = 'Josh Perez';
const element = <h1>Hello, {name}</h1>;
```

#### JSX是一个表达式

可以在jsx中赋值给变量。作为参数传入

```jsx
function formatName(user) {
  return user.firstName + ' ' + user.lastName;
}

const user = {
  firstName: 'Harper',
  lastName: 'Perez'
};

const element = (
  <h1>
    Hello, {formatName(user)}!
  </h1>
);
function getGreeting(user) {
  if (user) {
    return <h1>Hello, {formatName(user)}!</h1>;
  }
  return <h1>Hello, Stranger.</h1>;
}
		
```



#### JSX中置顶属性

```

```



#### 使用JSX指定子元素



#### JSX防止注入攻击



#### 表示对象



=====

### 元素渲染

React 元素是创建开销极小的普通对象。React DOM 会负责更新 DOM 来与 React 元素保持一致

React DOM 会负责更新 DOM 来与 React 元素保持一致。

更新已渲染的元素

计时器的例子



### 组件&Props

定义组件最简单方式编写JS函数

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

ES6 的 class

```jsx
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

自定义组件

```jsx
const element = <Welcome name="Sara" />;
```

组合组件

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

function App() {
  return (
    <div>
      <Welcome name="Sara" />     
      <Welcome name="Cahal" />    
      <Welcome name="Edite" />    
    </div>
  );
}
```

提取组件

将组件拆分成更小组件

参考下面代码

```jsx
function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <img className="Avatar"
          src={props.author.avatarUrl}
          alt={props.author.name}
        />
        <div className="UserInfo-name">
          {props.author.name}
        </div>
      </div>
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```



1. 提取 Avatar 组件

```jsx
function Avatar(props) {
  return (
    <img className="Avatar"      src={props.user.avatarUrl}      alt={props.user.name}    />  );
}
```

修改 Avatar放入代码中

```jsx
function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <Avatar user={props.author} />        <div className="UserInfo-name">
          {props.author.name}
        </div>
      </div>
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```



提取 UserInfo 组件 将Avatar 放入 UserInfo中渲染

```jsx
function UserInfo(props) {
  return (
    <div className="UserInfo">      <Avatar user={props.user} />      <div className="UserInfo-name">        {props.user.name}      </div>    </div>  );
}
```

进一步简化 Comment 组件

```jsx
function Comment(props) {
  return (
    <div className="Comment">
      <UserInfo user={props.author} />      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```



Props 的只读性



### State&生命周期

State vs props

State: 隐形



**生命周期：**

挂载（mount）

卸载（unmount）

```jsx
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  componentDidMount() {  }
  componentWillUnmount() {  }
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
```

**这些方法叫做“生命周期方法”。**

```jsx
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  componentDidMount() {
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }

  componentWillUnmount() {
    clearInterval(this.timerID);
  }

  tick() {    this.setState({      date: new Date()    });  }
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Clock />);
```



**如何使用state**

```jsx
// Wrong
this.state.comment = 'Hello';
```

```jsx
// Correct
this.setState({comment: 'Hello'});
```

难点： this 关键词的使用

因为 `this.props` 和 `this.state` 可能会异步更新，所以你不要依赖他们的值来更新下一个状态。

例如，此代码可能会无法更新计数器：

```jsx
// Wrong
this.setState({
  counter: this.state.counter + this.props.increment,
});
```

```jsx
// Correct
this.setState((state, props) => ({
  counter: state.counter + props.increment
}));
```

```jsx
// Correct
this.setState(function(state, props) {
  return {
    counter: state.counter + props.increment
  };
});
```

### 

### State 的更新会被合并

```jsx
  constructor(props) {
    super(props);
    this.state = {
      posts: [],      comments: []    };
  }
```

```jsx
 componentDidMount() {
    fetchPosts().then(response => {
      this.setState({
        posts: response.posts      });
    });

    fetchComments().then(response => {
      this.setState({
        comments: response.comments      });
    });
  }
```

这里的合并是**浅合并**，所以 `this.setState({comments})` 完整保留了 `this.state.posts`， 但是完全替换了 `this.state.comments`。

## 

**数据向下流**

不管是父组件或是子组件都无法知道某个组件是有状态的还是无状态的，并且它们也并不关心它是函数组件还是 class 组件。

这就是为什么称 state 为局部的或是封装的的原因。除了拥有并设置了它的组件，其他组件都无法访问。

组件可以选择把它的 state 作为 props 向下传递到它的子组件中：

```jsx
<FormattedDate date={this.state.date} />
```

`FormattedDate` 组件会在其 props 中接收参数 `date`，但是组件本身无法知道它是来自于 `Clock` 的 state，或是 `Clock` 的 props，还是手动输入的：

```jsx
function FormattedDate(props) {
  return <h2>It is {props.date.toLocaleTimeString()}.</h2>;
}
```

像瀑布，向下流动

**证明**每个组件都是真正独立的，我们可以创建一个渲染三个 `Clock` 的 `App` 组件：

```jsx
function App() {
  return (
    <div>
      <Clock />      
      <Clock />      
      <Clock />    
    </div>
  );
}
```





### 事件处理

React 元素的事件处理和 DOM 元素的很相似，但是有一点语法上的不同：

- React 事件的命名采用小驼峰式（camelCase），而不是纯小写。
- 使用 JSX 语法时你需要传入一个函数作为事件处理函数，而不是一个字符串。

传统js 事件处理和 react的事件处理

```html
<button onclick="activateLasers()">
  Activate Lasers
</button>
```

```jsx
<button onClick={activateLasers}>  Activate Lasers
</button>
```



在 React 中另一个不同点是你不能通过返回 `false` 的方式阻止默认行为。你必须显式地使用 `preventDefault`。例如，传统的 HTML 中阻止表单的默认提交行为，你可以这样写：

```jsx
<form onsubmit="console.log('You clicked submit.'); return false">
  <button type="submit">Submit</button>
</form>
```

```jsx
function Form() {
  function handleSubmit(e) {
    e.preventDefault();    console.log('You clicked submit.');
  }

  return (
    <form onSubmit={handleSubmit}>
      <button type="submit">Submit</button>
    </form>
  );
}
```

`e` 是一个合成事件。React 根据 [W3C 规范](https://www.w3.org/TR/DOM-Level-3-Events/)来定义这些合成事件，所以你不需要担心跨浏览器的兼容性问题。React 事件与原生事件不完全相同。如果想了解更多，请查看 [`SyntheticEvent`](https://zh-hans.reactjs.org/docs/events.html) 参考指南

```jsx
class Toggle extends React.Component {
  constructor(props) {
    super(props);
    this.state = {isToggleOn: true};

    // 为了在回调中使用 `this`，这个绑定是必不可少的    this.handleClick = this.handleClick.bind(this);  }

  handleClick() {    this.setState(prevState => ({      isToggleOn: !prevState.isToggleOn    }));  }
  render() {
    return (
      <button onClick={this.handleClick}>        {this.state.isToggleOn ? 'ON' : 'OFF'}
      </button>
    );
  }
}
```

使用 React 时，你一般不需要使用 `addEventListener` 为已创建的 DOM 元素添加监听器。事实上，你只需要在该元素初始渲染的时候添加监听器即可。

```jsx
class Toggle extends React.Component {
  constructor(props) {
    super(props);
    this.state = {isToggleOn: true};

    // 为了在回调中使用 `this`，这个绑定是必不可少的    this.handleClick = this.handleClick.bind(this);  }

  handleClick() {    this.setState(prevState => ({      isToggleOn: !prevState.isToggleOn    }));  }
  render() {
    return (
      <button onClick={this.handleClick}>        {this.state.isToggleOn ? 'ON' : 'OFF'}
      </button>
    );
  }
}
```



向事件处理程序传递参数



### 条件渲染

React 中的条件渲染和 JavaScript 中的一样，使用 JavaScript 运算符 [`if`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/if...else) 或者[条件运算符](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Conditional_Operator)去创建元素来表现当前的状态，然后让 React 根据它们来更新 UI。

```jsx
function UserGreeting(props) {
  return <h1>Welcome back!</h1>;
}

function GuestGreeting(props) {
  return <h1>Please sign up.</h1>;
}
```

```jsx
function Greeting(props) {
  const isLoggedIn = props.isLoggedIn;
  if (isLoggedIn) {    return <UserGreeting />;  }  return <GuestGreeting />;}
const root = ReactDOM.createRoot(document.getElementById('root')); 
// Try changing to isLoggedIn={true}:
root.render(<Greeting isLoggedIn={false} />);
```

**元素变量**

```jsx
class LoginControl extends React.Component {
  constructor(props) {
    super(props);
    this.handleLoginClick = this.handleLoginClick.bind(this);
    this.handleLogoutClick = this.handleLogoutClick.bind(this);
    this.state = {isLoggedIn: false};
  }

  handleLoginClick() {
    this.setState({isLoggedIn: true});
  }

  handleLogoutClick() {
    this.setState({isLoggedIn: false});
  }

  render() {
    const isLoggedIn = this.state.isLoggedIn;
    let button;
    if (isLoggedIn) {      button = <LogoutButton onClick={this.handleLogoutClick} />;    } else {      button = <LoginButton onClick={this.handleLoginClick} />;    }
    return (
      <div>
        <Greeting isLoggedIn={isLoggedIn} />        {button}      </div>
    );
  }
}

const root = ReactDOM.createRoot(document.getElementById('root')); 
root.render(<LoginControl />);
```

增加了 &&运算符 和 三目运算符



### 列表&Key

首先，让我们看下在 Javascript 中如何转化列表。

```javascript
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map((number) => number * 2);console.log(doubled);
```

```jsx
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>    <li>{number}</li>  );  return (
    <ul>{listItems}</ul>  );
}

const numbers = [1, 2, 3, 4, 5];
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<NumberList numbers={numbers} />);
```



JS

Promise

### 表单



### 状态提升



### 组合&继承



Css的布局

控制div靠左或靠右的排版布局,我整理三种平时用到的css属性小知识

**1、float属性**

**2、position属性**

**3、align-self属性**

加id react hook 

https://plainenglish.io/blog/the-useid-hook-in-react-18-take-a-look

Flex & Grid

2017 更加迅速lay out align distribute space

main idea: 给容器改变 item 宽高的能力，这样可以更好适应空间布局

Flex针对应用的不同组件, 小规模的布局

Grid 适合大规模布局

FlexBox的一些术语

main axis Main-start | main-end main size | cross axis cross-start cross-end cross size

display direction order flex-grow flex-warp flex-shrink





Align items 纵轴

 align content 

justify content 主轴



React的变化

props 变化 或者 state的变化 会自动更新变化

React的underfine

解构的写法



## Using the State Hook

 a new addition in React 16.8. They let you use state and other React features without writing a class.





### React哲学 ****





## React on Trello

JS Unit Testing Basic & React Component Testing Basic

why 单元测试  开发之中无缘无故的bug

单元测试测什么： Function Object Class Module

How: Test Input -> Function ->{Test Failed, Test Passed} 3A: Arrange, Act, Assert

B站密码验证规则 长度6-10位 必须包含字母和数字  如何手动测试

单元测试是最好的开发文档。 

测试工具： [快速开始 · Jest (jestjs.io)](https://jestjs.io/zh-Hans/docs/getting-started)

why choose Jest. 

另配置 优秀的API支持 轻松 Mock 快速且安全

Jest CLI 

Jest my-test.js jest-watch jest --coverage

认识Jest断言

expect(result).matcher(expected);

匹配器 Matchers

![image-20220925141022186](/Users/zhiwen.shithoughtworks.com/Library/Application Support/typora-user-images/image-20220925141022186.png)



**React Components Test 组件测试**

什么是组件测试

多个单元测试组合成了组件测试

测试组件的外在行为

e.g. 验证码为例子 1:DOM 元素是否被正确渲染 2:与外界的交互

如何测试组件

![image-20220925141810638](/Users/zhiwen.shithoughtworks.com/Library/Application Support/typora-user-images/image-20220925141810638.png)

React testing library

其中核心库 testing-library-dom 轻量级web网页测试解决方案

查询DOM节点与之交互来测试网页

[Introduction | Testing Library (testing-library.com)](https://testing-library.com/docs/)



function components 更简单的一种写组件的方式





































































### 
