# Nesting Navigators

<p>在手机app中通常都是由各式各样的navigation组成,在React Navigation中路由(routers)和navigators是组合使用的，这样便能满足app更复杂的navigation结构。</p>
<p>在聊天app中，通常需要在第一个场景中放置几个表格来展示最近的聊天或者所有联系人。</p>

## Tab Navigator 介绍

从建立一个新的`TabNavigator`，文件名`App.js`:

```javaScript
import { TabNavigator } from "react-navigation";

class RecentChatsScreen extends React.Component {
  render() {
    return <Text>List of recent chats</Text>
  }
}

class AllContactsScreen extends React.Component {
  render() {
    return <Text>List of all contacts</Text>
  }
}

const MainScreenNavigator = TabNavigator({
  Recent: { screen: RecentChatsScreen },
  All: { screen: AllContactsScreen },
});
```

<p>如果`MainScreenNavigator`在navigator组件的最上层，那么结果则是：</p>

*** Android *** ![android](https://reactnavigation.org/assets/examples/simple-tabs-android.png)
*** iPhone *** ![iPhone](https://reactnavigation.org/assets/examples/simple-tabs-iphone.png)
## 在屏幕中镶嵌Navigator

<p>当我们只想让选项Tabs在第一个场景中可见，在新的场景到来的时候将选项Tabs覆盖住。</p>
<p>
新建一个Tab Navigator，将最上层的场景命名为`StackNavigator`，使其效果达到[上一步的效果](https://code.csdn.net/weixin_36570478/native-navigation/wikis/Home)。</p>

```javaScript
const SimpleApp = StackNavigator({
  Home: { screen: MainScreenNavigator },
  Chat: { screen: ChatScreen },
});
```
<p>由于`MainScreenNavigator`被视为是一个场景，我们便可以给它一个`navigationOptions`：由于`MainScreenNavigator`被视为是一个场景，我们便可以给它一个`navigationOptions`：</p>

```javaScript
MainScreenNavigator.navigationOptions = {
  title: 'My Chats',
};
```
<p>为了便于演示，我们可以在每个Tab为了便于演示，我们可以在每个Tab Navigator布局里添加一个按钮，通过按钮连接到聊天场景：</p>

```javaScript
<Button
  onPress={() => this.props.navigation.navigate('Chat', { user: 'Lucy' })}
  title="Chat with Lucy"
/>
```

<p>现在我们就已经把一个navigator嵌入另一个navigator中了，我们可以在两个navigator中`navigate`了：现在我们就已经把一个navigator嵌入另一个navigator中了，我们可以在两个navigator中`navigate`了：</p>

*** Android *** ![android](https://reactnavigation.org/assets/examples/nested-android.png)
*** iPhone *** ![iPhone](https://reactnavigation.org/assets/examples/nested-iphone.png)
