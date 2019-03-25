# SawayChihiro
千与千寻动画展示

本章节会主要讲解 Adobe Animate CC 的脚本使用，虽然做动画也是Ancc的强项，但是这不是我的强项，在翻阅了大量的资料和询问了很多热心的人后，我完成了一个比较好看的作品，虽然这个作品还未完全完成，也确实存在许多瑕疵，但是为了避免更多人走弯路，我想把这段时间的经验和踩过的坑分享给需要的人。

----

#### 软件的下载和安装与破解

首先不推荐使用`Adobe Animate cc 2017` 以上更高的版本，因为我曾经在2019中使用脚本发现，无法使用实例访问子节点实例，后来知道是因为加了屏障的缘故，这是在2019发现的问题。由于2017更加稳定，所以我比较推荐使用这个版本的工具进行开发。

##### 下载

[2017 下载地址]: 链接：https://pan.baidu.com/s/1OlNeoG8eZKqTZaqiGA2N6w	"ddzm"

##### 安装与破解

安装就是下一步一直操作，破解在提供的下载压缩包中，解压后会有一个 `破解文件` 将文件覆盖到你的ancc的安装路径即可破解。 

----

#### 一切从新建开始

##### 创建一个ActionScript3.0工程

![1553527517925](C:\Users\99405\AppData\Roaming\Typora\typora-user-images\1553527517925.png)

类型选择 `ActionScript3.0`,选择这个的目的是因为我们可以直接使用`swf`进行预览和调试，如果你选择了`HTML5 Canvas`，那么进行预览和调试的时候会弹出浏览器进行这些操作，相对来说比较麻烦，设置导出来也是`js`与`html`的打包文件，因为本身是通过`Canvas`进行实现的，所以难免会有些卡顿，我比较了两种导出后的结果后发现，`swf`更加流畅，而且导出后，也只有一个`swf`文件，它和浏览器也是完美兼容的，这是我选择他理由，而且最关键的是，我们需要使用`ActionScript3.0`脚本进行控制动画的各种切换、暂停、播放。

##### 界面介绍

![1553528493108](C:\Users\99405\AppData\Roaming\Typora\typora-user-images\1553528493108.png)

> 舞台区域
>
> > 舞台区域就是对你目前工程预览的地方
>
> 时间轴	    
>
> > 如果你熟悉ps或者sai等绘图或者图片软件，对这个界面应该不陌生，他就是在这基础之上添加了时间的概念，可以叠加多个图层。
>
> 工具区域
>
> > Ancc的主要功能是用来做动画，所有这里的许多工具都是为了对图片或者视频进行剪辑和动画而存在的，但是今天我主要说的是文本工具，这也是我用的最多的工具



----

#### 元件

##### 什么是元件

我的个人理解，你所使用的所有资源：例如图片、视频、文字需要享有能够具有动画能力的时候，我们需要把她们转化为`元件` 。成为元件的资源，可以有非常丰富的动画效果，例如移动，放大缩小，渐变，改变文字内容等，所以一句话概括就是： `元件是Adobe Animate CC 中的动画组件` 。

##### 按钮

我们可以选择任意一个被我们拖进舞台的图片或者自己编辑的文字，右键他们选择`转化为元件` 。

这个时候，我们可以选择让这个元件成为`按钮`或者`影片剪辑` 

![1553529247793](C:\Users\99405\AppData\Roaming\Typora\typora-user-images\1553529247793.png)

成为按钮后，双击已经被转化为元件的按钮，可以修改他们在不同事件类型下的状态。

![1553529487730](C:\Users\99405\AppData\Roaming\Typora\typora-user-images\1553529487730.png)

##### 影片剪辑

影片剪辑同样可以做成按钮，但是影片剪辑的功能会更加强大一些，它可以将一个视频，或者说一组非常多的图整合到时间轴的一帧中去，类似一个文件夹，然后你可以通过脚本来控制这个“文件夹”什么时候播放，什么时候暂停，从哪一帧暂停，哪一帧开始。

 至于为什么要在这里引入脚本的概念是因为，影片剪辑要实现和按钮一样悬停与点击的视觉效果，需要使用脚本来切换帧数来达到和按钮一样的视觉效果。



----



#### ActionScript3.0 部分API讲解

![1553529988624](C:\Users\99405\AppData\Roaming\Typora\typora-user-images\1553529988624.png)

这个按钮在你右键任意一帧动画时选择`动作 `选项就会弹出脚本编辑框，有一对尖括号地方为`代码片段` ，这个里面收录了所有目前为止ActionScript支持的api，双击某一树节点，就会给出模版介绍，非常方便，这里主要来给大家介绍几个比较常见的api。

###### 事件（Event）

```javascript
//此方法为ActionScript中的事件监听函数，第一个参数为事件的类型，第二为具体的方法
addEventListener(MouseEvent.CLICK,function(me:MouseEvent):void{});
```

###### 跳转（Goto）

```java
gotoAndStop(_label:String);
gotoAndStop(frameNumber:Number);//String 类型的参数为给帧数填写的标签，Number参数为具体帧数

gotoAndPlay(_label:String);
gotoAndPlay(frameNumber:Number);
//gotoAndStop方法表示，跳转到指定帧数并停止播放。
//gotoAndPlay方法表示，跳转到指定帧数并开始播放。

Stop();//立刻暂停
Play();//立刻开始
```

此外需要额外声明的是，事件函数在按钮和影片剪辑都可以使用，但是跳转方法却只能在影片剪辑使用，这也很好理解，因为只有`影片` 才存在暂停和播放。



----



#### 在ancc中播放视频

想要在ancc中使用视频是一件比较麻烦的事情，因为它只识别`.flv` 的视频文件，其它类型的文件在库中都会直接黑屏，无法正常播放，更可能无法直接添加到舞台中预览。

##### 如何转化

思路是，`mp4`->`wmv` ->`flv`

至于为什么要这样转化，我现在做出解释，首先，我们的最终目的是想要转化为`.flv`格式的视频文件，大部分直导入视频格式都会报出`.H264`的错误，这都是因为格式不被支持的原因，首先经过的我的测试，需要使用`Adobe Media Encoder`进行转化的`.flv` 支持的最好，而`Adobe Media Encoder`能支持转化的文件类型为`.wmv`格式，所以就会有了以上的思路，其它情况下我也出现了拖入工程中出现黑屏的结果。

需要注意的是，使用的`Adobe Media Encoder`最好使用`MediaEncoderCS4`这一版本，更高的版本，很容易崩溃，反正我的多次重装卸载还是无法运行。

我的顺序是先使用`格式工坊`将视频文件变为`WMV`，然后使用`Adobe Media Encoder`转化为`.flv`.

[MediaEncoderCS4]: 链接：https://pan.baidu.com/s/1hblpZI8ezoxQCLlU4rZjcA	"ayc4"



----



#### 在ancc中控制音频

起初，这个音频真的让我头疼一晚上，如果是放在视频中还好，但要作为背景音乐来控制是非常麻烦的，首先是你无法单独控制音频的播放和暂停，还有即便你将它放入影片剪辑中，即便你stop了他，他还是会播放，不受控制，原因是音频作为特殊的流，他无法被放入影片剪辑中进行操控，而真正想要操控他，需要使用`链接`让他成为`实例`并且得到他的`音频通道`才可以。

![1553531714558](C:\Users\99405\AppData\Roaming\Typora\typora-user-images\1553531714558.png)

这表示，我们希望使用脚本来将它加载到舞台中来，并且获得该音频的控制权，这个`TestSound`就是一个别名，我们需要`new`写上我们定义名字。

```javascript
import flash.media.Sound;
import flash.media.SoundChannel;

//获得实例对象
var mySound:Sound=new TestSound() as Sound;
var sndChannel:SoundChannel = mySound.play();
//对循环播放的操作
sndChannel.addEventListener(Event.SOUND_COMPLETE,rePlaySound);
function rePlaySound(e:Event):void
{mySound.play();}
```

###### 暂停

非常遗憾的是，我们无法对这个`mySound`进行单独的暂停，虽然他提供一个`close`方法，但是你一旦使用了这个方法，会导致如同字面意思般，流将会关闭，你也无法再继续使用。

那么真的就无法暂停了吗，答案是不是的，`ActionScript`提供了一个我个人觉得不是很恰当但是也能用的api

```javascript
SoundMixer.stopAll();
```

这个方法比较极端，就是关闭当前场景的所有声音，特别说明的是，这个说的暂停是指不记录播放位置的，也就是说，你一旦暂停后，你的下一次`play`将会从头开始。

#### 作品展示

我的作品放在的git上，喜欢的小伙伴可以下载试玩一下~

[千与千寻](https://github.com/PopCandier/SawayChihiro.git)







