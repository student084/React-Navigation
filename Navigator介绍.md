## Navigators
<p>
Navigators 允许你定义自己的app导航结构，Navigators也负责绘制头部(headers)和选择栏
(tab bars)，依您的配置参数而定。
</p>
<p>
在底层，navigators是一个空白的React控件。
</p>

## 建立Navigators
<p>`react-navigation`有以下几个函数建立方式：</p>

 * [StackNaigator](#)-每次描绘一个场景并且提供场景切换动画。每当一个新的场景打开，新场景便会位于栈顶。
 * [TabNavigator](#)-描绘一个选择栏让用户在几个场景中实现切换。
 * [DrawerNavigator](#)-提供一个位于场景左侧的抽屉栏。

## 通过Navigators描绘场景

描绘app场景的navigator只是一些React控件。
<p>
创造一个场景可以通过如下方法：
</p>

* 场景的`navigation`参数，允许场景调用navigation方法，比如打开另一个场景
* 场景的`navigationOptions`可以提供导航里目前场景的定制（比如:头部标题、选择栏标签等）
## 在顶层组件中调用导航
<p>万一你想在同级别的Navigator Screen中调用Navigator，建议使用`ref`选项:</p>

```javaScript
const AppNavigator = StackNavigator(SomeAppRouteConfigs);
class App extends React.Component {
  someEvent() {
    // call navigate for AppNavigator here:
    this.navigator && this.navigator.dispatch({ type: 'Navigate', routeName, params });
  }
  render() {
    return (
      <AppNavigator ref={nav => { this.navigator = nav; }}/>
    );
  }
}
```
<p>注意，这种方法只能在顶层的navigator中使用。</p>

## Navigation Containers
<p>
当navigation建立的navigator参数消失的时候，navigators会表现得像是顶层的navigators一样
。这种设计提供了一个透明的navigation container，它是顶层navigation的来源。
</p>

<p>
当绘制一个被包含的navigators时，navigation prop是可选的。当其不存在时，container进入
并且管理自己的navigation状态。它也处理URLs,额外的链接及Android上的返回按钮。
</p>

<p>
为了方便，内置的navigators有这个能力，因为在场景前使用了`createNavigatonContainer`
。通常，navigators需要一个navigaton prop去使用这个函数。
</p>
<p>
最上层的navigator接受如下参数：
</p>

### `onNavigationStateChange(prevState, newState, action)`

<p>
每次navigator管理的navigation状态改变时调用。它接受以前的状态，新的navigation状态
和状态改变时的问题动作。默认为在控制台中打印状态的改变。
</p>

### `uriPrefix`

<p>
app可能处理的URIs前缀。当处理一个深层的额外路由连接时会被使用。
</p>


