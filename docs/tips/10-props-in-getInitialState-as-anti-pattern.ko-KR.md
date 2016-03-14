---
id: props-in-getInitialState-as-anti-pattern-ko-KR
title: getInitialState의 Props는 안티패턴
layout: tips
permalink: props-in-getInitialState-as-anti-pattern-ko-KR.html
prev: componentWillReceiveProps-not-triggered-after-mounting-ko-KR.html
next: dom-event-listeners-ko-KR.html
---

> 주의 : 
>
> 이것은 React에만 국한된 팁이 아니고 안티패턴은 평범한 코드 속 에서도 종종 발생합니다. 이 글에서는 React로 간단하게 설명해 보겠습니다.

부모로부터 받은 props를 이용하여 `getInitialState`에서 state를 생성할 때 종종 "진실의 소스", 예를 들어 진짜 데이터가 있는 곳을 중복으로 만들 때가 있습니다. 왜냐하면 `getInitialState`는 컴포넌트가 처음 만들어질 때만 호출되기 때문입니다.

가급적이면 나중에 싱크가 맞지 않거나 유지보수 문제를 발생시키지 않도록 값을 필요할 때 계산하세요.


**나쁜 예제:**

```js
var MessageBox = React.createClass({
  getInitialState: function() {
    return {nameWithQualifier: 'Mr. ' + this.props.name};
  },

  render: function() {
    return <div>{this.state.nameWithQualifier}</div>;
  }
});

ReactDOM.render(<MessageBox name="Rogers"/>, mountNode);
```

더 나은 코드:

```js
var MessageBox = React.createClass({
  render: function() {
    return <div>{'Mr. ' + this.props.name}</div>;
  }
});

ReactDOM.render(<MessageBox name="Rogers"/>, mountNode);
```

(복잡한 로직이라, 메소드에서 계산하는 부분만 떼어 왔습니다.)

하지만 여기서 prop이 컴포넌트 내부에서 조정되는 상태의 초기값일 뿐임이 명확하다면, 이것은 안티 패턴이 **아닙니다.**

```js
var Counter = React.createClass({
  getInitialState: function() {
    // initial로 시작하는 메소드는 내부에서 받은 어떠한 값을 초기화 할 목적이 있다는 것을 나타냅니다.
    return {count: this.props.initialCount};
  },

  handleClick: function() {
    this.setState({count: this.state.count + 1});
  },

  render: function() {
    return <div onClick={this.handleClick}>{this.state.count}</div>;
  }
});

ReactDOM.render(<Counter initialCount={7}/>, mountNode);
```
