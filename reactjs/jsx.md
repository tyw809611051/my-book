#### 定义
> JavaScript的语法扩展,描述用户界面

#### 使用方法
- 使用JavaScript表达式

```
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

ReactDOM.render(
  element,
  document.getElementById('root')
);
```

- if语句

```
function getGreeting(user) {
  if (user) {
    return <h1>Hello, {formatName(user)}!</h1>;
  }
  return <h1>Hello, Stranger.</h1>;
}
```


#### 注意事项
- 大括号包裹的 JavaScript 表达式时就不要再到外面套引号了
```
#错误
const element = <img src="{user.avatarUrl}"></img>;
#正确
const element = <img src={user.avatarUrl}></img>;
```

- 如果 JSX 标签是闭合式的，那么你需要在结尾处用 />
```
const element = <img src={user.avatarUrl} />;
```

- 因为 JSX 的特性更接近 JavaScript 而不是 HTML , 所以 React DOM 使用 camelCase 小驼峰命名 来定义属性的名称，而不是使用 HTML 的属性名称
例如，class 变成了 className，而 tabindex 则对应着 tabIndex.