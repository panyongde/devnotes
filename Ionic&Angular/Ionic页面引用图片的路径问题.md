在 Ionic 项目中，我们平时一般都是在文件夹 `src/` 里编写代码，如果用到一些静态的图片，一般都会放在 `src/assets/images/` 里，如果我们在页面中使用图片，比如页面 `src/pages/home/home.heml` 使用图片：

```html
# src/pages/home/home.heml
<img src="../../assets/images/pic.png" />
```

在浏览器运行项目：

```shell
～ ionic serve
```

这是浏览器中的页面能正常显示图片，但在连上真机运行，发现图片不能显示。原因在于：

使用以下命令添加运行平台后

```shell
～ codava platform add android --nofetch
```

增加了目录 `platforms`，我们代码被编译到 `platforms/android/asssets/www` 下，这个目录下的结构和 `src` 下的结构有些差异，通过观察，要是图片能在真机上正常显示，写图片路径时需注意：

1. 在 page 页面插入图片，不需要 `../../` ，应该按下面路径写：

```html
# src/pages/home/home.heml
<img src="assets/images/pic.png" />

# 或者
<div style="background: url('assets/images/icon/tongzhi.png') no-repeat"></div>
```

2. 如果是在 css 文件加入背景图片，需要这么写：

```scss
background: url('../assets/images/homeBG.png') no-repeat left top;
```

