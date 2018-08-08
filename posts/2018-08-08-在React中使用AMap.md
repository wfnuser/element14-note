---

title: 在React中使用AMap
date: 2018-08-08

---

## 前言
最近入职了阿里，没想到又开始做起了前端的工作，目前组内前端技术栈为react。新任务需要用到[AMap](https://lbs.amap.com/)于是研究了一下如何将两者集成，这里做一下记录。

## React AMap
首先搜了一下是否有别人的实现，很幸运eleme前端团队实现了一个被验证下来还挺好用的封装：[react-amp](https://github.com/ElemeFE/react-amap)。

如果只需要接入地图而不需任何交互的话是非常简单的，在npm install相关包之后只需要如下简短的几行代码即可实现效果。
```
import { Map } from 'react-amap';
export default class GeoSelector extends Component {
  render() {
    return (
            <Map>
            </Map>
    );
  }
}
```

我们这边主要需要做一个封装好的经纬度选择器，所以需要与地图进行交互，翻越了一下源代码找到了组件封装的事件入口。具体使用方法如下：
```
import { Map } from 'react-amap';
export default class GeoSelector extends Component {
  amapEvents = {
    click: e => {
      this.setState({
        lng: e.lnglat.getLng(),
        lat: e.lnglat.getLat(),
        visible: false,
      });
      this.props.form.setFieldsValue({
        longitude: this.state.lng,
        latitude: this.state.lat,
      });
    },
  };
  render() {
    return (
            <Map events={this.amapEvents}>
              <Geolocation {...pluginProps} />
            </Map>
    );
  }
}
```

实现过程中还碰到了一些坑，主要是因为对react哲学和基本概念理解还不到位，比如碰到了在render函数中setState会无限触发react的渲染机制等问题。同样在组件封装的过程中也没有很好的控制数据的流向，在调用组件的过程中是有侵入的。主要问题在于子组件的state需要被父组件的其他子组件状态所控制。
还有一个workaround的地方，代码里使用了antd的form组件，为了setFieldsValue在组件中放置了两个空的getFieldDecorator修饰的空span。

之后如果有机会对react-amap的源码进行深入研究后会再更新本文。
