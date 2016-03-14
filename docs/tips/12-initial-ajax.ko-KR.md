---
id: initial-ajax-ko-KR
title: AJAX를 통해 초기 데이터 읽어오기
layout: tips
permalink: initial-ajax-ko-KR.html
prev: dom-event-listeners-ko-KR.html
next: false-in-jsx-ko-KR.html
---

`componentDidMount`에서 데이터를 가져옵니다. 응답이 올 때 데이터가 state에 저장되고 렌더링을 시작하여 UI를 갱신합니다.

데이터를 비동기적으로 가져올 때는 `componentWillUnmount`를 사용하여 컴포넌트가 마운트 해제되기 전에 남아있는 요청을 취소합니다.

이 예제는 희망하는 Github 사용자의 최근 gist를 가져옵니다.

```js
var UserGist = React.createClass({
  getInitialState: function() {
    return {
      username: '',
      lastGistUrl: ''
    };
  },

  componentDidMount: function() {
    this.serverRequest = $.get(this.props.source, function (result) {
      var lastGist = result[0];
      this.setState({
        username: lastGist.owner.login,
        lastGistUrl: lastGist.html_url
      });
    }.bind(this));
  },

  componentWillUnmount: function() {
    this.serverRequest.abort();
  },

  render: function() {
    return (
      <div>
        {this.state.username}'s last gist is
        <a href={this.state.lastGistUrl}>here</a>.
      </div>
    );
  }
});

ReactDOM.render(
  <UserGist source="https://api.github.com/users/octocat/gists" />,
  mountNode
);
```
