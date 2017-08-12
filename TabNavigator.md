## TabNavigator
<p>
TabNavigator快速建立一个含有几个选择栏和一个路由选择器的场景，[官方demo](https://exp.host/@react-navigation/NavigationPlayground)
</p>

```javaScript
class MyHomeScreen extends React.Component {
  static navigationOptions = {
    tabBarLabel: 'Home',
    // Note: By default the icon is only shown on iOS. Search the showIcon option below.
    tabBarIcon: ({ tintColor }) => (
      <Image
        source={require('./chats-icon.png')}
        style={[styles.icon, {tintColor: tintColor}]}
      />
    ),
  };

  render() {
    return (
      <Button
        onPress={() => this.props.navigation.navigate('Notifications')}
        title="Go to notifications"
      />
    );
  }
}

class MyNotificationsScreen extends React.Component {
  static navigationOptions = {
    tabBarLabel: 'Notifications',
    tabBarIcon: ({ tintColor }) => (
      <Image
        source={require('./notif-icon.png')}
        style={[styles.icon, {tintColor: tintColor}]}
      />
    ),
  };

  render() {
    return (
      <Button
        onPress={() => this.props.navigation.goBack()}
        title="Go back home"
      />
    );
  }
}

const styles = StyleSheet.create({
  icon: {
    width: 26,
    height: 26,
  },
});

const MyApp = TabNavigator({
  Home: {
    screen: MyHomeScreen,
  },
  Notifications: {
    screen: MyNotificationsScreen,
  },
}, {
  tabBarOptions: {
    activeTintColor: '#e91e63',
  },
});
```
## API定义
<p>
`TabNavigator(RouteCofigs, TabNavigatorConfig)`
</p>
### RouteConfigs
<p>
路由配置对象，路由名到路由配置的映射，告诉navigator当前的路由，see [example](https://reactnavigation.org/docs/api/navigators/StackNavigator.md#routeconfigs) from 
`StackNavigator`。
</p>

### TabNavigatorConfig

* `tabBarComponent`-用来做选择栏的组件，比如`TabBarBottom`(iOS default)，
`TabBarTop`(Android default)
* `tabBarPosition`-选择栏位置，可以为'top'或者'bottom'
* `swipeEnable`-是否允许在选择间切换
* `animationEnabled`-改变选择时是否需要动画
* `lazy`-是否采用只在需要的时候临时渲染，而不是提前渲染
* `tabBarOptions`-配置选择栏，具体将在下方提及。
几个传递到底层路由器，修改导航逻辑的参数
* `initRouteName`-定义选择栏首次加载时的路由名
* `order`-定义选择栏排序的路由名数组
* `paths`-提供一个从路由名到地址配置的映射，它在routeConfing中被覆盖
* `backBahavior`-返回键是否引起选择栏位置置于初始的选择状态？如果是，设为`initalRoute`,
否则设为`none`。默认为`initialRoute`的行为。
### `tabBarOptions` for `TabBarBottom`（iOS默认的选择栏）

* `activeTintColor`-活跃标签的lable和icon的颜色
* `activeBackgroundColor`-活跃标签的背景色
* `inactiveTintColor`-非活跃标签的lable和icon颜色
* `inactiveBackgroundColor`-非活跃标签的背景色
* `showLabel`-是否显示标签栏label，默认为true
* `style`-标签栏样式
* `labelStyle`-选择栏标签样式
* `tabStyle`-标签样式

<p>
Example:
</p>

```javaScript
tabBarOptions: {
  activeTintColor: '#e91e63',
  labelStyle: {
    fontSize: 12,
  },
  style: {
    backgroundColor: 'blue',
  },
}
```
### `tabBarOptions` for `TableBarTop`（Android 默认标签栏）

* `activeTintColor`-活跃标签的label和icon颜色
* `inactiveTintColor`-非活跃标签的label和icon颜色
* `showIcon`-是否展示标签图标,默认false
* `showLabel`-是否展示标签的label
* `upperCaseLabel`-label是否大写，默认true
* `pressColor`-按压时的波纹颜色(Android 5.0以上可用)
* `pressOpacity`-被按压标签的不透明度(iOS和Android 5.0以下支持）
* `scrollEnable`-是否标签栏可滚动标签
* `tabStyle`-标签样式
* `indicatorStyle`-标签指示器样式(底部标签)
* `labelStyle`-标签label样式
* `iconStyle`-标签图标样式
* `style`-标签栏样式
<p>
例子：
</p>

```javaScript
tabBarOptions: {
  labelStyle: {
    fontSize: 12,
  },
  tabStyle: {
    width: 100,    
  },
  style: {
    backgroundColor: 'blue',
  },
}
```
## 场景导航选项
### `title`
<p>
可作为`headerTitle`和`tabBarLabel`后备的通用标题
</p>
### `tabBarVisible`
<p>
是否显示标签栏，默认为true
</p>
### `tabBarIcon`
<p>
React元素，或者含有`{focused: boolean, tintColor:string}`,且返回值为React元素的方法
，此元素将显示在导航栏上
</p>
### `tabBarLabel`
<p>
在导航栏上显示的标题字符串或者是React元素，或者是含有`{focused: boolean, tintColor:string}`,且返回值为React元素的方法
，此元素将显示在导航栏上。入果没有定义则为场景`title`。
若要隐藏，查看之前的`tabBarOptions.showLabel`。
</p>
## 导航参数
<p>
由`TabNavigator(...)`方法创造的导航组件，属性如下：
</p>

* `screenProps`-传递给子场景和导航选项额外的选项，例如：
```javaScript
onst TabNav = TabNavigator({
  // config
});
<TabNav
  screenProps={/* this prop will get passed to the screen components as this.props.screenProps */}
/>
```