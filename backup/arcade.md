# arcade窗口

arcade 程序需要创建一个窗口来承载各种内容，通过窗口类 Window 即可创建。

```python
from arcade import *

w = Window()
run()
```

但为了后续方便扩展自己需要的功能，一般会定义一个自己的类，继承 arcade 的 Window 类，然后在我们类的 init 方法中使用 super
方法代表父类，调用父类的 init 方法完成窗口创建。
后续即可添加各种方法实现自己要的功能。

```python
from arcade import *


class Room(Window):
    def __init__(self):
        super().__init__()


r = Room()
run()
```

# Sprite精灵

在 arcade 中，所有出现在窗口中的元素都可以用 sprite 类生成，比如背景、人物、动物等等。我们还可以通过程序控制它们进行移动、旋转、跳跃等等。
因为 sprite 是精灵的意思，所以后续我们也就直接叫这些元素为精灵。
Sprite 类的使用方法很简单，先写下类名和括号，然后在括号里传入第一个参数，是一个图片，用来确定这个精灵长什么样子。
最后将生成的精灵对象保存到一个变量中即可。

```python
bg = Sprite("room.png")
```

我们一般会在 init 初始化方法中生成精灵，然后保存到属性中，方便在其它方法中使用这些精灵。

```python
from arcade import *


class Room(Window):
    def __init__(self):
        super().__init__()
        self.bg = Sprite("room.png")


r = Room()
run()
```

# on_draw()

on_draw() 方法专门用来处理精灵的展示，是 arcade 程序的基本组成之一。
在方法里调用精灵的 draw 方法就可以将精灵绘制到窗口中进行展示。

```python
from arcade import *


class Room(Window):
    def __init__(self):
        super().__init__()
        self.bg = Sprite("room.png")

    def on_draw(self):
        self.bg.draw()


r = Room()
run()
```

另外，不需要我们在任何地方调用 on_draw 方法，因为 run 函数里已经帮我们调用了。

# 鼠标点击

on_mouse_press() 方法在鼠标按下时会被调用，可以用来实现鼠标点击的交互，比如打印点击位置的坐标。
定义时，除了第一个固定参数 self，还有其它几个固定参数要写。
首先分别是 x 和 y，它们代表当前鼠标点击位置的坐标。
接着是 button，这是按钮的意思，代表鼠标按下的是哪个按键，左键呢，中键呢，还是右键。
不过无论是哪个键被按下，arcade 都会帮我们调用 on mouse press 方法。
最后是 modifiers，这个一般用不到，可以先不管。

```python
def on_mouse_press(self, x, y, button, modifiers):
    print(x, y)
```

写好定义的格式后，就可以实现鼠标点击后要发生什么了。

# 图片翻转

load texture 函数可以实现图片翻转
水平翻转

```python
load_texture(图片名称, mirrored=True)
```

垂直翻转

```python
load_texture(图片名称, flipped=True)
```

水平+垂直翻转

```python
load_texture(图片名称, mirrored=True， flipped = True)
```


# 生成造型

```python
load_texture(图片名称)
```

通过图片生成造型。

#设置窗口大小和标题
调用 Window 类中的 init 方法，分别传入三个参数，它们分别是窗体的宽度、高度和标题，可以设置窗体。

```python
Window(窗体宽度, 窗体高度, 窗体标题)
```

示例：

```python
from arcade import *


class MyWindow(Window):
    def __init__(self):
        super().__init__(400, 700, "飞船试飞")
```

# 精灵的位置属性

精灵的位置属性有这些，center_x 和 center_y 表示精灵的中心点 x 坐标和 y 坐标

| 精灵的属性    | 意义          |
|----------|-------------|
| center_x | 精灵的中心点 x 坐标 |
| center_y | 精灵的中心点 y 坐标 |
| position | 精灵的中心点坐标    |
| top      | 精灵的上边界 y 坐标 
|

on_update 和 on_draw 一样一直被 run 调用，与 on_draw 不同，on_update 有一个参数 time。

```python
from arcade import *


class MyWindow(Window):
    def __init__(self):
        super().__init__(400, 700, "飞船试飞")
        # 背景
        self.bg = Sprite("sky.png")
        self.bg.position = 200, 350

    def on_draw(self):
        self.bg.draw()

    def on_update(self):
        print("update")


w = MyWindow()
run()
```

# 清除窗口绘制

Window 类中的 clear() 方法可以清除窗口的绘制

```python
clear()
清除窗口的绘制
```

# 添加造型

Sprite 类中的 append_texture 方法可以添加精灵对象的造型

```python
精灵对象.append_texture(load_texture(图片名称))
```

使用 Sprite 创建精灵对象时使用的图片生成造型，是第一个造型，索引为 0，第二次添加的造型索引为 1，如果还有添加的造型，依次递增...

# 设置造型

Sprite 类中的 set_texture 方法可以设置精灵对象的造型

```python
精灵对象.set_texture(造型的索引)
```

# 精灵的缩放

通过 Sprite 的参数 scale 可以对精灵进行缩放，scale 大于 1 表示放大，小于 1 表示缩小。
方式一：核心代码

```python
# 时空之门
self.door = Sprite("door1.png", scale=0.4)
```

方式二：核心代码

```python
# 时空之门
self.door = Sprite("door1.png")
self.door.scale = 0.4
```

# 获取精灵对象的宽度

通过精灵对象的 width 属性可以获取到精灵对象的宽度；height 可以获取到精灵对象的高度。

```python
精灵对象.width
精灵对象.height
```

# 检测精灵与精灵的碰撞

check_for_collision 函数用于判断精灵 sprite1 是否与精灵 sprite2 发生碰撞，如果发生碰撞返回 True，否则返回
False。默认使用的是矩形碰撞检测法。

```python
check_for_collision(sprite1, sprite2)
```

# 鼠标移动事件

on_mouse_motion 方法在鼠标移动的时候会被调用，参数 x 表示鼠标在窗口中移动后的 x 坐标，y 表示鼠标在窗口中移动后的 y 坐标，dx
表示鼠标移动后 x 坐标与鼠标移动前 x 的差值， dy 表示鼠标移动后 y 坐标与鼠标移动前 y 的差值。

```python
on_mouse_motion(self, x, y, dx, dy)
```

说明：
• dx > 0：鼠标向右移动，dx < 0：鼠标向左移动
• dy > 0：鼠标向上移动，dy < 0：鼠标向下移动

# AnimatedTimeSprite

AnimatedTimeSprite 类是继承于 Sprite 类的一种精灵类，因此它具有 Sprite 的所有属性和方法，除此之外，它还具有自己独有的方法
update animation，作用是每隔一段时间间隔就自动更换精灵的造型。

更换精灵造型

```python
AnimatedTimeSprite对象.update_animation()
```

扩展：
如果每隔造型之间切换的时间太快，修改AnimatedTimeSprite 的 texture_change_frames 属性可以设置造型切换的时间间隔，默认为
5。数值越大，切换的时间间隔越长。

# 精灵列表

使用 SpriteList 可以创建精灵列表，精灵列表中的元素为精灵对象，需要注意，使用 SpriteList 创建精灵列表时不需要参数。

```python
# 子弹
bullet_list = SpriteList()
```

SpriteList 的常用方法

| SpriteList类中的方法 | 作用             |
|-----------------|----------------|
| append(精灵对象)    | 添加一个精灵对象到精灵列表中 |
| draw()          | 绘制精灵列表中的精灵     |
| update()        | 更新精灵列表中的精灵     |
| remove(精灵对象)    | 从精灵列表中移出精灵对象   |

# 精灵对象.update

精灵对象的 change x 和 change y 属性，它们表示坐标的变化量，需要配合精灵对象的 update 方法使用，每次调用精灵对象的 update
方法时，精灵对象的中心点 x 坐标 center x 就会改变 change x，中心点 y 坐标 center y 就会改变 change y。
说明：
精灵对象.change_x：精灵对象的中心点 x 坐标在调用 update() 后的变化量
精灵对象.change_y：精灵对象的中心点 y 坐标在调用 update() 后的变化量

# schedule

schedule 函数可以给指定的函数设定调用的时间间隔，设定后，函数就会按照设定的时间间隔不断的被调用。

```python
schedule(函数名或者方法名, 时间间隔)
```

有一个特别需要注意的地方就是 schedule 函数的第一个参数是函数名或者方法名，对这个函数的格式是有要求的，它必须有一个参数，并且只能有一个参数，参数名可以自己定义，通常我们使用
time，它表示上一次执行这个函数或者方法所花费的时间。

# 将精灵对象移出精灵列表

精灵对象的 kill 方法可以把精灵对象自己移出所在的精灵列表

```python
精灵对象.kill()
```

# 绘制文本

```python
draw_text(需要绘制的文本, x坐标, y坐标, 颜色, 字体大小, font_name=("simhei", "PingFang"))
```

arcade 中使用 draw text 函数绘制文本，前五个参数依次是需要绘制的文本，x坐标，y坐标，颜色，字体大小，除此之外还需要指定字体，这样做是为了确保绘制中文的时候在
Windows 或者 Mac 系统能够正常显示出来。如果没有绘制中文的话，可以不指定字体。
注意：需要绘制的文本数据类型为字符串。
常见颜色常量

| 颜色名称      | arcade 中的颜色常量 |
|-----------|---------------|
| red（红）    | color.RED     |
| white（白）  | color.WHITE   |
| black（黑）  | color.BLACK   |
| green（绿）  | color.GREEN   |
| yellow（黄） | color.YELLOW  |
| blue（蓝）   | color.BLUE    |
| purple（紫） | color.PURPLE  |
| gray（灰）   | color.GRAY    |
| brown（棕）  | color.BROWN   |
| tan（褐色）   | color.TAN     |
| pink（粉红色） | color.PINK    |

# unschedule

与 schedule 对应，unschedule 用来取消使用 schedule 设置的函数，取消后，函数不再按照 schedule 设定的时间间隔被调用。

```python
unschedule(schedule设置的函数 / 方法名)
```

# 播放音频

pyglet.media 是处理音频的模块，本次课，我们用到了其中的 Player、load 和 StaticSource 这三中工具。
loda 用来加载音频文件。
若想减少播放音频的延迟，可以用 StaticSource 处理一下，处理后的音频还能绑定到多个 Plyaer 实例上。
Player 是一个类，用来控制音频，用 queue 方法把加载的音频绑定到 Player 上，用 play 方法就能播放音频了。

# 鼠标点击事件

在 Arcade 里边，侦测鼠标点击事件要用到 on_mouse_press 方法。除了 self 之外，这个方法带四个参数。和 on_mouse_motion 方法一样，x
和 y 也表示鼠标的坐标，button 表示按下的鼠标键，而 modifiers 表示键盘修饰键，比方说 ctrl、shift 这些，是和鼠标按键形成组合用的。
Arcade 还提供了侦测角色列表中的角色是否和某个坐标点重合的函数：get_sprites_at_point。
这个函数的返回值是一个列表，里边包含了在侦测坐标点的所有精灵。

# 重置游戏(再来一次）

重置游戏的关键在于从游戏过程中 被改变的那些值中，找到需要改回初始状态的值，在飞机大战中，我们找了以下需要重置的值，并放到了
setup 方法中。

# View 类

Arcade 提供了 View 类，可以为一个 Window 实例提供多个界面。
想要让 View 类切换界面，使用 show_view 方法，on_show 切换到一个界面时，会默认调用 View 类中的 on_show 方法，所以把切换后才需要启动的部分，放到
on_show 方法里边。

