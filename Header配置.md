## Configuring the Header

Header 只在StackNavigator中有效。</br>
在演示的例子中，我们建立了一个StackNavigator来播放几个场景的app。
</br>
当导航跳转到chat场景时，我们可以通过navigate方法为这个新的路由定义一些参数。在这个
例子中，我们想为chat场景提供联系人的名字:

```javaScript
this.props.navigation.navigate('Chat', { user:  'Lucy' });
```
参数`user`将能够在chat场景中获得：

```javaScript
class ChatScreen extends React.Component {
  render() {
    const { params } = this.props.navigation.state;
    return <Text>Chat with {params.user}</Text>;
  }
}
```
## 设置Header标题

然后，头部(header)标题也可以通过场景参数来配置：

```javaScript
class ChatScreen extends React.Component {
  static navigationOptions = ({ navigation }) => ({
    title: `Chat with ${navigation.state.params.user}`,
  });
  ...
}
```
<div>
<a style="display:inline-block">Android<img src='https://reactnavigation.org/assets/examples/basic-header-android.png' padding-top=65px padding-left=18px width=312px height=629px/></a>
<a style="display:inline-block">iPhone<img src='https://reactnavigation.org/assets/examples/basic-header-iphone.png' padding-top=65px padding-left=18px width=312px height=629px/></a>
</div>

## 添加右部按钮

通过navigation option我们可以在`header`里添加一个右部按钮：

```javaScript
static navigationOptions = {
  headerRight: <Button title="Info" />,
  ...
```
<div>
<a style="display:inline-block">Android<img src='https://reactnavigation.org/assets/examples/header-button-android.png' padding-top=65px padding-left=18px width=312px height=629px/></a>
<a style="display:inline-block">iPhone<img src='https://reactnavigation.org/assets/examples/header-button-iphone.png' padding-top=65px padding-left=18px width=312px height=629px/></a>
</div>

navigation options可以被定义成一个navigation prop,下例通过路由参数渲染了一个不同的button，并且
点击按钮会调用`navigation.setParms`：

```javaScript
static navigationOptions = ({ navigation }) => {
  const {state, setParams} = navigation;
  const isInfo = state.params.mode === 'info';
  const {user} = state.params;
  return {
    title: isInfo ? `${user}'s Contact Info` : `Chat with ${state.params.user}`,
    headerRight: (
      <Button
        title={isInfo ? 'Done' : `${user}'s info`}
        onPress={() => setParams({ mode: isInfo ? 'none' : 'info'})}
      />
    ),
  };
};
```

现在，头部可以与场景的路由和状态互动了

<div>
<a style="display:inline-block">Android<img src='https://reactnavigation.org/assets/examples/header-interaction-android.png' padding-top=65px padding-left=18px width=312px height=629px/></a>
<a style="display:inline-block">iPhone<img src='https://reactnavigation.org/assets/examples/header-interaction-iphone.png' padding-top=65px padding-left=18px width=312px height=629px/></a>
</div>
了解更多header options信息，见于[navigation options document][1]。
[1]:https://reactnavigation.org/docs/navigators/navigation-options#Stack-Navigation-Options