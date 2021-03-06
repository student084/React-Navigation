## Hello Mobile Navigation
以建立一个非常简单的Android和ios聊天app开始
## 运行与安装

* 首先，确认您已经将React Native的环境配置齐全，然后建立一个新的项目并
添加`react-navigation`:

```javaScript
# Create a new React Native App
react-native init SimpleApp
cd SimpleApp

# Install the latest version of react-navigation from npm
npm install --save react-navigation

# Run the new app
react-native run-android # or:
react-native run-ios
```
* 判别是否成功建立这个空的app，如果成功则有如下效果：

<div>
<a style="display:inline-block">*** Android ***<img src='https://reactnavigation.org/assets/examples/bare-project-android.png' padding-top=65px padding-left=18px width=312px height=629px/></a>
<a style="display:inline-block">*** iPhone ***<img src='https://reactnavigation.org/assets/examples/bare-project-iphone.png' padding-top=65px padding-left=18px width=312px height=629px/></a>
</div>

* 我们希望ios和Android能共享代码，所以我们接下来要删除`index.ios.js`和`index.androdi.js`
里面的内容，并将内容替换为`import'./App'`。

* 为了app的正常启动，我们创建一个新的文件`App.js`。

## Stack Navigator介绍

* 在这个app中，我们将使用`StackNavigator`，因为我们想贯彻一个'栈(stack)'导航概念，在
这个栈中每个新的场景会添加到栈顶，返回时则从栈顶移除。先从单个的场景开始：

```javaScript
import React from 'react';
import {
  AppRegistry,
  Text,
} from 'react-native';
import { StackNavigator } from 'react-navigation';

class HomeScreen extends React.Component {
  static navigationOptions = {
    title: 'Welcome',
  };
  render() {
    return <Text>Hello, Navigation!</Text>;
  }
}

const SimpleApp = StackNavigator({
  Home: { screen: HomeScreen },
});

AppRegistry.registerComponent('SimpleApp', () => SimpleApp);
```
* 场景的`title`在静态的`navigationOptions`中是可配置的，`navigationOptions`中可以
为导航(navigator)中当前的场景设置许多配置。

* 现在，同样的场景又能显示了：

<div>
<a style="display:inline-block">*** Android ***<img src='https://reactnavigation.org/assets/examples/first-screen-android.png' padding-top=65px padding-left=18px width=312px height=629px/></a>
<a style="display:inline-block">*** iPhone ***<img src='https://reactnavigation.org/assets/examples/first-screen-iphone.png' padding-top=65px padding-left=18px width=312px height=629px/></a>
</div>



## 添加新的场景

* 在`App.js`文件中，添加一个组件`ChatScreen`:

```javaScript
class ChatScreen extends React.Component {
  static navigationOptions = {
    title: 'Chat with Lucy',
  };
  render() {
    return (
      <View>
        <Text>Chat with Lucy</Text>
      </View>
    );
  }
}
```
* 然后在`HomeScreen`中添加一个`Button`，通过`Button`点击，利用`routeName``Chat`
联接到`ChatScreen`。

```javaScript
class HomeScreen extends React.Component {
  static navigationOptions = {
    title: 'Welcome',
  };
  render() {
    const { navigate } = this.props.navigation;
    return (
      <View>
        <Text>Hello, Chat App!</Text>
        <Button
          onPress={() => navigate('Chat')}
          title="Chat with Lucy"
        />
      </View>
    );
  }
}
```
* 使用navigate方法根据场景导航的属性跳转到`ChatScreen`,在使用navigate方法跳转
前，必须要将`ChatScreen`加入`StackNavigator`中才能有效：

```javaScript
const SimpleApp = StackNavigator({
  Home: { screen: HomeScreen },
  Chat: { screen: ChatScreen },
});
```
* 现在则能在导航中进入或退出新的场景了：

<div>
<a style="display:inline-block">*** Android ***<img src='https://reactnavigation.org/assets/examples/first-navigation-android.png' padding-top=65px padding-left=18px width=312px height=629px/></a>
<a style="display:inline-block">*** iPhone ***<img src='https://reactnavigation.org/assets/examples/first-navigation-iphone.png' padding-top=65px padding-left=18px width=312px height=629px/></a>
</div>


## 参数传递
* 在`ChatScreec`里硬编码一个名字并不明智，如果能渲染传递过来的名字将会更有实用
性，so let's do that.
* 除了在navigate方法里定义目标场景的`routeName`外，我们还能传递新场景里需要用到
的一些参数。首先，我们将通过`HomeScreen`组件传递`user`参数到路由中去。

```javaScript
class HomeScreen extends React.Component {
  static navigationOptions = {
    title: 'Welcome',
  };
  render() {
    const { navigate } = this.props.navigation;
    return (
      <View>
        <Text>Hello, Chat App!</Text>
        <Button
          onPress={() => navigate('Chat', { user: 'Lucy' })}
          title="Chat with Lucy"
        />
      </View>
    );
  }
}
```
* 然后再在`ChatScreen`组件中显示我们通过路由传递过来的`user`参数。

```javaScript
class ChatScreen extends React.Component {
  // Nav options can be defined as a function of the screen's props:
  static navigationOptions = ({ navigation }) => ({
    title: `Chat with ${navigation.state.params.user}`,
  });
  render() {
    // The screen's current route is passed in to `props.navigation.state`:
    const { params } = this.props.navigation.state;
    return (
      <View>
        <Text>Chat with {params.user}</Text>
      </View>
    );
  }
}
```
* 现在你可以在导航到Chatscreen里时看到传过来的name了。试着修改`HomeScreen`中的`user`参数，see what happens!

<div>
<a style="display:inline-block">*** Android ***<img src='https://reactnavigation.org/assets/examples/first-navigation-android.png' padding-top=65px padding-left=18px width=312px height=629px/></a>
<a style="display:inline-block">*** iPhone ***<img src='https://reactnavigation.org/assets/examples/first-navigation-iphone.png' padding-top=65px padding-left=18px width=312px height=629px/></a>
</div>
