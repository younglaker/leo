---
layout: post
title: React Learning Record
date: 2019-09-08 08:24:00
category: [React]
tags: [React, React Native]
---

## Start

```
npm i -g create-react-app@1.5.2
create-react-app react-app
```

<!--more-->

Inside that directory, you can run several commands:

```
  yarn start
    Starts the development server.

  yarn build
    Bundles the app into static files for production.

  yarn test
    Starts the test runner.

  yarn eject
    Removes this tool and copies build dependencies, configuration files
    and scripts into the app directory. If you do this, you can’t go back!

```

## Bootstrap

```
 npm i -s bootstrap@4.1.1
```

`index.js`

```
import 'bootstrap/dist/css/bootstrap.css';
```

## export

Add `Component/counter.jsx` to `src`

```
export default class Counter extends Component {

  render() {}
}
```

equals:

```
class Counter extends Component {

  render() { }
}
export default Counter;
```

## ReactDOM.render

In `index.js`, it render th `App.js`

```
import App from './App';

ReactDOM.render(<App />, document.getElementById('root'));
```

can be repalced by this to render Counter.js :

```
import Counter from './components/counter';

ReactDOM.render(<Counter />, document.getElementById('root'));
```

## Use component

In `App.js`,add:

```
  return (
    <div className="App">
      ...
      <Counter />
    </div>
  );
```

## React.Fragment

If use <div>, there is a useless element

![](https://raw.githubusercontent.com/aomine-sama/px/master/2019/19090801.png)

If delete <div>
![](https://raw.githubusercontent.com/aomine-sama/px/master/2019/19090802.png)

Use `<React.Fragment>` instead:

![](https://raw.githubusercontent.com/aomine-sama/px/master/2019/19090803.png)

## State

```

export default class Counter extends Component {
  state = {
    count: 0
  };
  render() {
    return (
      <React.Fragment>
        <span>{this.state.count}</span>
      </React.Fragment>
    );
  }
}
```

## Function return and expression

```
  state = {
    count: 0
  };
  render() {
    return (
      <React.Fragment>
        <div>{this.formatCount()}</div>
      </React.Fragment>
    );
  }

  formatCount() {
    return this.state.count === 0 ? 'Zero' : this.state.count;
  }
```

Eauqls to :

```
  formatCount() {
    const { count } = this.state;
    return count === 0 ? 'Zero' : count;
  }
```

![](https://raw.githubusercontent.com/aomine-sama/px/master/2019/19090804.png)

We can also insert elements and variable:

```
  formatCount() {
    const { count } = this.state;
     const x = <h1>Zero</h1>
    return count === 0 ? x : count;
  }
```

## Image src

```
  state = {
    imageUrl: 'https://picsum.photos/200'
  };
  render() {
    return (
      <React.Fragment>
        <img src={this.state.imageUrl} alt="" />
      </React.Fragment>
    );
  }
```

![](https://raw.githubusercontent.com/aomine-sama/px/master/2019/19090805.png)

## Use Bootstrap CSS

Be sure to use `className`, not `class`

```
<div className="badge badge-primary m-2">{this.formatCount()}</div>
<button className="btn btn-secondary btn-sm">Increcement</button>
```

![](https://raw.githubusercontent.com/aomine-sama/px/master/2019/19090806.png)

## Inline CSS

```
<div style={{ fontSize: 30 }} className="badge badge-primary m-2">Zero</div>
```

Or:

```
  aaa = { fontSize: 30 };
  render() {
    return (
      <React.Fragment>
        <div style={ this.aaa } className="badge badge-primary m-2">Zero</div>
      </React.Fragment>
    );
  }
```

![](https://raw.githubusercontent.com/aomine-sama/px/master/2019/19090807.png)

## Dynamic class name

```
  render() {
    return (
      <React.Fragment>
        <div className={this.getBadgeClasses()}>
          Zero
        </div>
    );
  }
  getBadgeClasses() {
    let classes = 'badge m-2 badge-';
    classes += this.state.count === 0 ? 'warning' : 'primary';
    return classes;
  }
```

![](https://raw.githubusercontent.com/aomine-sama/px/master/2019/19090808.png)

![](https://raw.githubusercontent.com/aomine-sama/px/master/2019/19090809.png)

## For loop

```
  state = {
    tags: ['tag1', 'tag2', 'tag3']
  };

```

```
<ul>
      {this.state.tags.map(tag => (
        <li>{tag}</li>
      ))}
 </ul>
```

![](https://raw.githubusercontent.com/aomine-sama/px/master/2019/19090810.png)

Add key:

```
<ul>
    {this.state.tags.map(tag => (
    <li key={tag}>{tag}</li>
    ))}
</ul>
```

or

> It there is more than one parameter, add `( )`

```
<ul>
    {this.state.tags.map((tag, index) => (
    <li key={index}>{tag}</li>
    ))}
</ul>
```

![](https://raw.githubusercontent.com/aomine-sama/px/master/2019/19090811.png)

## Render after if

> If return more one line, add `( )`

```
render() {
  return (
    <React.Fragment>
      {this.renderTags()}
    </React.Fragment>
  );
}

renderTags() {
  if (this.state.tags.length === 0)
    return <p>No tasgs</p>;

  return (
    <ul>
      {this.state.tags.map((tag, index) => (
        <li key={index}>{tag}</li>
      ))}
    </ul>
  );
}
```

## Expression `&&`

```
render() {
  return (
    <React.Fragment>
      {this.renderTags()}
      {this.state.tags.length !== 0 && 'There are tags'}
    </React.Fragment>
  );
}
```

![](https://raw.githubusercontent.com/aomine-sama/px/master/2019/19090812.png)

## Event

`onClick`, not `onclick`

```
<button onClick={this.handleIncrement}>Increcement</button>

handleIncrement(e) {
  console.log(e);
}
```

> Event need to be sent function without parameter

**Right:**

```
<button onClick={this.handleIncrement}>
```

**Wrong:**

```
//this.handleIncrement ( 1 ) is not a functon
<button onClick={this.handleIncrement ( 1 ) }>
```

**Right:**

```
<button onClick={this.doHandleIncrecement }>

  doHandleIncrecement=()=>{
    this.handleIncrement({id: 1})

  }
  handleIncrement = (item) => {
    console.log(item.id);
  };
```

**Right ( recommend ) :**

```
<button onClick={() => this.handleIncrement({ id: 1 })}>

handleIncrement = item => {
  console.log(item.id);
};
```

## this, constructor()

We can't call `this` in function:

```
  handleIncrement() {
    console.log(this);
  }
```

![](https://raw.githubusercontent.com/aomine-sama/px/master/2019/19090813.png)

Use `constructor()` to bind this,

```
  constructor() {
    super();
    console.log(this);
    this.handleIncrement = this.handleIncrement.bind(this);
  }

  handleIncrement(e) {
    console.log(this);
  }
```

Or use `Arrow Function`

```
  handleIncrement = () => {
    console.log(this);
  };
```

![](https://raw.githubusercontent.com/aomine-sama/px/master/2019/19090814.png)

## Updating state

**State**: starts with a default value when a Component mounts and then suffers from mutations in time. It is not advisable to store anything in a state that can be derived from props at any point in time

```
  handleIncrement = () => {
    this.setState({ count: this.state.count + 1 });
  };
```

> `this.state.count++` dosen't work

![](https://raw.githubusercontent.com/aomine-sama/px/master/2019/19090815.png)

## Passing data to components

**Props**: (short for properties) are a Component’s configuration. They are received from above and immutable.

`src/components/counters.jsx`

```
import Counter from './counter';

class Counters extends Component {
  state = {
    counInfo: [{ id: 1, val: 0 }, { id: 2, val: 5 }, { id: 3, val: 2 }]
  };
  render() {
    return (
      <div>
        {this.state.counInfo.map((item, index) => (
          <Counter key={index} id={item.id} value={item.val} />
        ))}
      </div>
    );
  }
}

export default Counters;
```

`src/components/counter.jsx`

```
  render() {
    console.log('props', this.props);
    return ();
  }
```

![](https://raw.githubusercontent.com/aomine-sama/px/master/2019/19090817.png)

Use props data in `src/components/counter.jsx`:
Put `state` in `constructor()`:

```
  // passing in props
  constructor(props) {
    super();

    // in constructor(), state need this，props dosen't need this
    this.state = {
      count: props.value,
      tags: ['tag1', 'tag2', 'tag3']
    };
  }
```

![](https://raw.githubusercontent.com/aomine-sama/px/master/2019/19090817.png)

## Passing children

`src/components/counters.jsx`

```
{this.state.counInfo.map((item, index) => (
  <Counter key={index} id={item.id} value={item.val}>
    <h4>title</h4>
  </Counter>
))}
```

`src/components/counter.jsx`

```
  render() {
    console.log('props', this.props);

    return (
      <div>
        ...
        {this.props.children}
      </div>
    );
  }
```

![](https://raw.githubusercontent.com/aomine-sama/px/master/2019/19090818.png)

![](https://raw.githubusercontent.com/aomine-sama/px/master/2019/19090819.png)

## React Developer Tools

![](https://raw.githubusercontent.com/aomine-sama/px/master/2019/19090820.png)

Refresh after installation, you can change the order:

![](https://raw.githubusercontent.com/aomine-sama/px/master/2019/19090829.png)

### 1

![](https://raw.githubusercontent.com/aomine-sama/px/master/2019/19090821.png)

![](https://raw.githubusercontent.com/aomine-sama/px/master/2019/19090822.png)

![](https://raw.githubusercontent.com/aomine-sama/px/master/2019/19090823.png)

## Props VS  State

- props: passing data, can't be modified

![](https://raw.githubusercontent.com/aomine-sama/px/master/2019/19090824.png)

- state: local, can't be visited by other components

## Passing function

`src/components/counters.jsx`

```
  render() {
    return (
      <div>
        ..
          <Counter
            ...
            onDelete={this.handleDelete}
          ></Counter>
        ..
      </div>
    );
  }

  handleDelete = () => {
    console.log('Handle delete ');
  };
```

`src/components/counter.jsx`

```
<button onClick={this.props.onDelete}>Delete</button>
```

## filter （Delete function）

`src/components/counter.jsx`

```
{/*  delete btn */}
<button
  onClick={() => this.props.onDelete(this.props.id)}
>
```

`src/components/counters.jsx`

```
<Counter
  ...
  onDelete={this.handleDelete}
  id={item.id}
>

handleDelete = countId => {
  const counInfo = this.state.counInfo.filter(c => c.id !== countId);

  // this.setState({ counInfo: countInfo });
  // we can omit the variable when the state parameter name is the same as the variable name
  this.setState({ counInfo });
};
```

## Removing local state

The state init only once when the component created, so it can't update when the props changes

```
    this.state = {
      count: props.value
    };
```

So, if want use the updating props data, deal the props in original component:

`src/components/counter.jsx`, use props instead of state :

```
{/* 增加按钮 */}
<button
  onClick={() => this.props.onIncrece(this.props.item)}
>
getBadgeClasses() {
  let classes = 'badge m-2 badge-';
  classes += this.props.item.val === 0 ? 'warning' : 'primary';
  return classes;
}

formatCount() {
  const count = this.props.item.val;
  return count == 0 ? 'Zero' : count;
}
```

`src/components/counters.jsx`, do increment in counters.jsx

```
<Counter
  ...
  onIncrece={this.handleIncrement}
>

handleIncrement = item => {
  // 拷贝state的counters
  const countInfo = [...this.state.countInfo];
  const index = countInfo.indexOf(item);
  countInfo[index] = { ...item };
  countInfo[index].val++;

  this.setState({ countInfo });
};
```

> 展开语法(Spread syntax),扩展运算符是三个点（...）。用于取出参数对象的所有可遍历属性，然后拷贝到当前对象之中
> https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Spread_syntax > https://www.cnblogs.com/it-Ren/p/10637904.html > ![](https://raw.githubusercontent.com/aomine-sama/px/master/2019/19090825.png)

## Life cycle

![](https://raw.githubusercontent.com/aomine-sama/px/master/2019/19090826.png)

order: constructor > render > componentDidMount

![](https://raw.githubusercontent.com/aomine-sama/px/master/2019/19090827.png)

- componentDidMount: After render, often initial ajax
- componentDidUpdate: after component updated, such as state, new props,often write ajax to get new data
- componentWillMount: before component removed, such as delete a component

Can check `prevProps` , `prevState` in `componentDidUpdate`:

```

  componentDidUpdate(prevProps, prevState) {
    console.log('prevProps', prevProps);
    console.log('prevState', prevState);
  }
```


![](https://raw.githubusercontent.com/aomine-sama/px/master/2019/19090829.png)

> Exchange blogroll： [http://laker.me/blog](http://laker.me/blog)
> Github：[https://github.com/younglaker](https://github.com/younglaker)
