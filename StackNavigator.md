## StackNavigator

<p>
StackNavigator提供了堆栈式的场景切换方式，切换时新场景将置于栈顶。
</p>
<p>
在默认的配置情况下StackNavigator切换场景的动画效果与ios或android的默认效果是相同的.
ios从右边滑入，android从底部褪去。在ios上StackNavigator也可以通过配置该变切换动画
，使其从底部滑落。
</p>

```javaScript
class MyHomeScreen extends React.Component {
  static navigationOptions = {
    title: 'Home',
  }

  render() {
    return (
      <Button
        onPress={() => this.props.navigation.navigate('Profile', {name: 'Lucy'})}
        title="Go to Lucy's profile"
      />
    );
  }
}

const ModalStack = StackNavigator({
  Home: {
    screen: MyHomeScreen,
  },
  Profile: {
    path: 'people/:name',
    screen: MyProfileScreen,
  },
});
```
## API Definiton
```javaScript
StackNavigator(RouteConfigs, StackNavigatorConfig)
```
## RouteConfigs

<P>
路由配置(The route config object)是一个包含从路由名字到路由具体配置信息的映射,
它将指导navigator如何呈现当前路由。
</P>

```javaScript
StackNavigator({

  // For each screen that you can navigate to, create a new entry like this:
  Profile: {

    // `ProfileScreen` is a React component that will be the main content of the screen.
    screen: ProfileScreen,
    // When `ProfileScreen` is loaded by the StackNavigator, it will be given a `navigation` prop.

    // Optional: When deep linking or using react-navigation in a web app, this path is used:
    path: 'people/:name',
    // The action and route params are extracted from the path.

    // Optional: Override the `navigationOptions` for the screen
    navigationOptions: ({navigation}) => ({
      title: `${navigation.state.params.name}'s Profile'`,
    }),
  },

  ...MyOtherRoutes,
});
```
## StackNavigatorConfig

<p>
路由选择：
</p>

* `initialRouteName`-为栈设置默认的场景，必须是路由配置里已经配置过的一个场景。
* `initialRouteParams`-初始路由参数
* `navigationOptions`-场景中需要使用的默认navigation选项
* `paths`-路由配置的地址映射（A mapping of overrides for the paths set in the route configs）

<p>
视觉选项：
</p>

* `mode`-定义渲染与动画样式,取值如下:
 * `card`-使用标准的ios和Android场景样式(default)
 * `modal`-使新场景从底部滑入，这是常见的ios样式，只在ios中有效，android无效
* `headerMode`-指定头部(header)的渲染效果，取值如下：
 * `float`-渲染一个停留在顶部的header，动画时不改动header，这是ios一种常见的模式
 * `screes`-每个场景都附有一个header,header的进出与场景一致，在Android中场用的模式
 * `none`-去除头部渲染
* `cardStyle`-使用这个属性覆盖或者扩充栈中个别card的默认样式
* `transitionConfig`-该方法返回一个动画对象用来覆盖默认的场景动画
* `onTransitionStart`-当card的切换动画即将开始时回调该方法
* `onTransitionEnd`-当card的切换动画完成时回调该方法


