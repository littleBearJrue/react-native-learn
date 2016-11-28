# 魅族手表

## 注意事项

- 不要在`render`中使用`this.setState()`
- `props`、`state`设置后不会马上变化，需要等到`render`后

```javascript
// 该方法可以在组件更新之后操作元素
void componentDidUpdate(object prevProps, object prevState)
```

- 子控件需要与父控件相同大小可以使用下面的style

```javascript
const style = {
  position: 'absolute',
  left: 0,
  top: 0,
  right: 0,
  bottom: 0,
};
```

## 导航栏
- title：导航栏标题文本
- leftImage：左侧按钮图片
- onLeftPress：左侧按钮回调方法
- rightImage：右侧按钮图片
- onRightPress：右侧按钮回调方法

```javascript
// 设置导航栏右侧分享按钮
const { navigator } = this.props;
const scenes = navigator.state.scenes || Immutable.fromJS({});
navigator.setState({
  scenes: scenes.set('walkDetailInfo', Immutable.fromJS({
    rightImage: require('../images/share_log.png'),
    onRightPress: () => navigator.push({ name: 'share' }),
  }))
});
```

## 屏幕适配
- scale: 缩放数值到当前设备合适的大小
- select: 选择距离当前设备屏幕最合适的值
- size: 当前屏幕尺寸，XS、S、M、L

```javascript
import { ScreenUtils } from '../utils';

const style = {
  // 小屏手机使用红色，其他使用蓝色
  color: ScreenUtils.select({
    S: 'red',
    M: 'blue',
  }),
  // 使用iPhone6即M为基准缩放，系数为XS: 0.72, S: 0.85, M: 1, L: 1.1
  marginTop: ScreenUtils.scale(20),
};
```

## BLE协议（[PDF](doc/智芯BLE协议.pdf)）

## 网络接口（[PDF](doc/魅族网络接口.pdf)）
- 获取用户数据：userInfo
- 更新用户数据：updateUser
- 同步手表信息：syncAdd
- 恢复手表信息：syncGet

```javascript
import { Network } from '../utils';

Network.userInfo({
  openId: 'hllohlkjcdkjk',
  token: 'kjkcdjkfdjkljf',
  type: Network.TYPE_WEIBO,
})
.then(userInfo => console.log('userInfo: ', userInfo))
.catch(error => console.warn(error));
```

## 基础知识

### [JavaScript](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript)
- [历史](http://www.ruanyifeng.com/blog/2011/06/birth_of_javascript.html)
- [编码规范](http://www.ituring.com.cn/article/197990)
- [ECMAScript 6](http://es6.ruanyifeng.com/)
- [High Order Component](https://leozdgao.me/chushi-hoc/)

### [React.js](https://facebook.github.io/react/docs/getting-started.html) / [中文](http://reactjs.cn/react/docs/getting-started.html) / [入门](https://hulufei.gitbooks.io/react-tutorial/content/introduction.html)
![react lifecycle](http://imgh.us/react-lifecycle.svg)

### [Redux](http://redux.js.org/) / [中文](http://cn.redux.js.org/)
![redux](https://raw.githubusercontent.com/lawrencebla/redux-review/master/react-redux.jpg)

### [React Native](http://facebook.github.io/react-native/docs/getting-started.html) / [中文](http://reactnative.cn/docs/)
- [Flexbox](http://facebook.github.io/react-native/docs/flexbox.html)
- [Native Module](http://facebook.github.io/react-native/docs/native-modules-android.html)
- [Native UI Components](http://facebook.github.io/react-native/docs/native-components-android.html)

### [Node.js](https://nodejs.org/)
- [learnyounode](http://www.kancloud.cn/kancloud/learnyounode/47115)
- [npm入门](http://aerotiger.info/archives/beginners-guide-node-package-manager.html)
