# HTML5 的常用元素与属性

## 保留的常用元素
HTML5并不是一种 革命式的发展，它是对HTML以前版本的继承和发展，因此HTML5保留了以前HTML版本的绝大部分标签。

### 基本元素
HTML 5保留的基本元素有如下几个。

- `<!-- ... -->:`定义HTML注释。位于`<!--`与`-->`之间的内容会被当成注释处理。
- `<html>`: 它是HTML 5文档的根元素。但HTML 5允许完全省略这个元素。
- `<head>`:它用于定义HTML 5文档的页面头部分。但HTML 5允许完全省略这个元素。
- `<title>`: 它用于定义HTML 5文档的页面标题。
- `<body>`:它用于定义HTML 5文档的页面主体部分，该标签可以指定id、class、 style
等核心属性，还可以指定onload、onunload、 onclick、 ondblclick、 onmousedown、onmouseup、onmouseover. onmousemove、onmouseout、onkeypress、onkeydown、onkeyup等事件属性，这些属性用于指定JavaScript脚本。

    注意:关于HTML5元素的事件属性，请参阅本书后面相关内容， 此处不会详细
    介绍这些事件属性的用法。后面介绍各标签时也不再详细列出各事件属性。
- `<style>`: 该元素用于引入样式定义。
- `<h1>`到 `<h6>`:定义标题一 到标题六。
- `<p>`: 定义段落，该标签可以指定id、class、style 等核心属性，还可以指定onclick等各种事件属性。

    提示:几乎所有的HTML元素都可指定id.style和class属性。其中id属性用于为:HTML元素指定一个唯一标识,该标识是通过DOM访问HTML元素的重要途径。| class和style属性是CSS样式相关属性

- `<br>`: 插入一个换行，该标签可以指定id、 class、 style等核心属性。
- `<hr>`:定义水平线,该标签可以指定id、class. style等核心属性,还可以指定onclick等各种事件属性。HTML 5中 hr 还代表了主题结束的语义。
- `<div>`: 定义文档中的节。该标签可以指定id、class、 style 等核心属性，还可以指定onclick等各种事件属性。
- `<span>`: 与div 基本相似，区别是该定义的节默认不会换行。该标签可以指定和div相同的属性。
