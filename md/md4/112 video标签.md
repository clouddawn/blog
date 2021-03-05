# video 标签

* **HTML` <video>` 元素** 用于在HTML文档中嵌入媒体播放器，支持文档内的视频播放。

## 属性

### autoplay

* 布尔属性；指定后，视频会马上自动开始播放，不会停下来等着数据载入结束。
* 属性兼容性不好，通常需要与 muted 属性配合使用，将视频静音之后放才可自动播放

### muted

* 设置后，音频会初始化为静音。

### controls

* 加上这个属性，[Gecko](https://baike.baidu.com/item/%E6%8E%92%E7%89%88%E5%BC%95%E6%93%8E/8371898?fromtitle=Gecko&fromid=7348782&fr=aladdin) 会提供用户控制，允许用户控制视频的播放，包括音量，跨帧，暂停/恢复播放。

### controlslist

* 当浏览器显示自己的控件集(例如，当指定了Controls属性时)，Controlslist属性将帮助浏览器选择在媒体元素上显示的控件。

* 允许接受的value有`nodownload`,`nofullscreen`和`noremoteplayback`
* 兼容性很差，只在 chrome 上可以使用

### loop

* 布尔属性；指定后，会在视频结尾的地方，自动返回视频开始的地方。

[**HTML Demo: <video>**](http://clouddawn.top/small-ideas/video/index.html)

[源代码](https://github.com/clouddawn/small-ideas/tree/main/video)

