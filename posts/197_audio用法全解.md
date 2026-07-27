# audio 用法全解

## 元素属性

* `controls`

  如果声明了该属性，浏览器将提供一个包含声音，播放进度，播放暂停的控制面板，让用户可以控制音频的播放。

* `loop`

  布尔属性；如果声明该属性，将循环播放音频。

* `src`

  嵌入的音频 URL。也可以在 audio 元素中使用 `<source>` 元素来替代该属性指定嵌入的音频。

## 方法

* `play()`

  开始播放音频。

* `pause()`

  暂停当前播放的音频。

## 属性

* `ended`

  返回音频的播放是否已结束

* `paused` 

  返回音频播放是否暂停

## 示例：实现循环播放

```html
<audio v-for="item in audio" :key="item.name" :ref="item.name" controls :src="item.source" ></audio>
<img id="playIcon" class="chenjingImg" src="@/assets/images/chenjing.jpg" alt="">
```

.

```js
let name = this.audio[this.currentPlayIndex].name;
let song = this.$refs[name][0];
let d_playIcon = document.getElementById("playIcon");
let that = this;

function play() {
    if (song.paused) {
        d_playIcon.className = "chenjingImg2";
    } else {
        d_playIcon.className = "chenjingImg";
    }
    if (song.ended) {
        if(that.currentPlayIndex === that.audio.length-1){
            that.currentPlayIndex = 0;
        }else {
            that.currentPlayIndex++;
        }
        name = that.audio[that.currentPlayIndex].name;
        song = that.$refs[name][0];
        that.$refs[name][0].play();
    }
}

setInterval(play, 200);

d_playIcon.addEventListener("click", function () {
    if (song.paused) {
        song.play();
    } else {
        song.pause();
    }
    play();
});
```

[源代码](https://github.com/clouddawn/audio-play-1/tree/main/audio1)



















