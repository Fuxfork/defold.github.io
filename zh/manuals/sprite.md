---
layout: manual
language: zh
github: https://github.com/defold/doc
title: 显示 2D 图片
brief: 本教程介绍了如何使用 sprite 组件显示 2D 图片和动画.
---

#  Sprites

Sprite 组件可以是屏幕上显示的简单图片或者逐帧动画.

![sprite](/manuals/images/graphics/sprite.png)

Sprite 组件使用 [图集](/zh/manuals/atlas) 或者 [瓷砖图源](/zh/manuals/tilesource) 进行图像显示.

## Sprite 属性

除了 *Id*, *Position* 和 *Rotation* 还有如下属性:

*Image*
: sprite所使用的图集或者瓷砖图源资源.

*DefaultAnimation*
: sprite的默认动画.

*Material*
: sprite的渲染材质.

*Blend Mode*
: 组件渲染时使用的混合模式.

*Size Mode*
: 如果设置为 `Automatic` 则编辑器会自动为 sprite 设置尺寸. 如果设置为 `Manual` 则可以手动设置尺寸.

*Slice 9*
: 设置在更改 sprite 大小时, 保留其周围边缘纹理的像素大小.

{% include shared/zh/slice-9-texturing.md %}

### 混合模式
{% include shared/zh/blend-modes.md %}

# 运行时操作

运行时可以使用各种各样的函数和属性 (参见 [API 文档](/ref/sprite/))来控制Sprite. 函数:

* `sprite.play_flipbook()` - 在sprite组件上播放动画.
* `sprite.set_hflip()` 和 `sprite.set_vflip()` - 翻转Sprite动画.

还可以使用 `go.get()` 和 `go.set()` 来控制Sprite:

`cursor`
: 初始化动画播放头 (`number`).

`image`
: sprite图 (`hash`). 可以通过 `go.set()` 方法使用图集或者瓷砖图集资源来修改此属性. 请参考 [这个例子的 API 文档](/ref/sprite/#image).

`material`
: sprite材质 (`hash`). 可以通过 `go.set()` 方法使用材质资源来修改此属性. 请参考 [这个例子的 API 文档](/ref/sprite/#material).

`playback_rate`
: 动画播放速率 (`number`).

`scale`
: Sprite缩放 (`vector3`).

`size`
: Sprite大小 (`vector3`). 只有 sprite 的 size-mode 设置为 manual 时可以更改.

## 材质常量

{% include shared/zh/material-constants.md component='sprite' variable='tint' %}

`tint`
: 3D网格颜色 (`vector4`). 四元数 x, y, z, 和 w 分别对应红, 绿, 蓝和不透明度.

## 材质属性

Sprite 可以覆盖当前分配材质中的顶点属性, 并将从组件传递到顶点着色器 (更多信息参见 [材质教程](/zh/manuals/material/#attributes)).

材质中指定的属性将在检查器中显示为常规属性, 并且可以在单个 Sprite 组件上设置. 如果任何属性被覆盖, 它将显示为被覆盖的属性, 并存储在磁盘上的 sprite 文件中:

![sprite-attributes](/manuals/images/graphics/sprite-attributes.png)

<div class='sidenote' markdown='1'>
自定义属性自从 Defold 1.4.8 版本可用!
</div>

## 相关项目配置

在 *game.project* 文件里有些关于Sprite的 [设置项目](/zh/manuals/project-settings#sprite).
