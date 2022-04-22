# 一、HTML常见元素和理解

## 1、HTML常见元素

### 1.1 head区元素（这部分不会在页面上留下直接内容）

- `meta`标签

  `meta`标签对整个网页有影响，会对网页**能否被搜索引擎检索**和在**搜索中的排名**起着关键作用。

  `meta`有一个必须属性为：`content`，表示需要设置的项的值。

  `meta`有两个非需要属性为：`http-equiv`和`name`，用于表示要设置的项

  - `http-equiv`属性：`http-equiv`一般设置的都是与http相关的信息，设置的值会关联到http头部。也就是说浏览器在请求服务器获取html的时候，服务器会将html中设置的meta放在响应头中返回给浏览器。常见的类型比如：`content-type`、`expires`、`refresh`、`set-cookie`、`charset`、`parama`等等

    - `content-type`：可以用来设置文档类型、设置字符集，如下，这样设置浏览器的头信息就会包含:

      `text/html charset=utf-8`

      ```html
      <meta http-equiv="content-type" content="text/html charset=utf-8">
      ```

    - `expires`：强缓存的标识字段，用于判断浏览器中缓存的资源是否过期，如下，表示到2022年12月31日资源过期。

      ```html
      <meta http-equiv="expires" content="31 DeC 2022">
      ```

    - `refresh`：该种设定表示5秒自动刷新并且跳转到指定的网页。如果不设置url的值那么浏览器则刷新本网页。

      ```html
      <meta http-equiv="refresh" content="5 url=http://www.zhiqianduan.com">
      ```

    - `window-target`：强制页面在当前窗口以独立页面显示, 可以防止别人在框架中调用自己的页面

      ```html
      <meta http-equiv="window-target" content="_top'>
      ```

    - `parama`：禁止浏览器从本地计算机的缓存中访问页面的内容

      ```html
      <meta http-equiv="parama" content+"no-cache">
      ```

  - `name`属性：主要用于描述网页，与对应的`content`中的内容主要是便于搜索引擎查找信息和分类信息用的, 用法与`http-equiv`相同，`name`设置属性名，`content`设置属性值。
    - `author`：标注网页的作者
    - `description`：告诉搜索引擎当前网页的主要内容，是关于网站的一段描述
    - `keywords`：设置网页的关键字，来告诉浏览器关键字是什么。是一个经常被用到的名称
    - `generator`：表示当前`html`是用什么工具编写生成的，并没有实际作用，一般是编辑器自动创建的。
    - `reviseed`：指定页面的最新版本
    - `robots`：告诉搜索引擎机器人抓取哪些页面，`all / none / index / noindex / follow / nofollow`

- `title`标签：定义文档的标题，**它是 `head` 部分中唯一必需的元素**。设置的内容不会显示在页面中，通常放置在浏览器窗户的标签栏或状态栏上。
  - `dir`属性：规定元素中内容的文本方向：rtl、ltr。
  - `lang`属性：规定元素中内容的语言代码。

- `style`标签：编辑内部样式的标签，里面写CSS样式代码
- `link`标签：`link`用于引入外部样式表，在`html`的头部可以包含任意数量的`link`，`link`标签有以下常用属性。
  - `type`：定义文档的类型。例如：`text/css`
  - `rel`：定义`html`文档和所要包含资源之间的链接关系，可能的值有很多，最为常用的是`stylesheet`，用于包含一个固定首选样式的表单。
  - `href`：指向被包含的url地址。
- `script`标签：加载`javascript`脚本的标签。加载的脚本会被默认执行。默认情况下当浏览器解析到`script`标签的时候会停止`html`的解析而开始加载`script`代码并且执行。
  - `type`：指定脚本的类型，例如：`text/javascript`
  - **`async`：规定是异步执行脚本，仅适用于通过`src`引入的外部脚本。设置的async属性的script加载不会影响后面html的解析，加载与html解析式同步发生的。加载完成后立即执行。执行后会停止html文档解析。**
  - `charset`：规定外部脚本文件汇总使用的字符编码
  - **`defer`：规定是否对脚本执行进行延迟，直到页面加载为止。设置了`defer`属性的`script`不会阻止后面`html`的解析，加载与解析是共同进行的，但是`script`的执行要在所有元素解析完成之后，`DOMContentLoaded`事件触发之前完成。**
  - `src`：外部脚本的引用文件。
- `base`标签

### 1.2 body区元素

- 行内元素：`a b span  strong em select(inline-block) img(inline-block) input(inline-block) button(inline-block)  textarea (inline-block) video(inline-block)  audio(inlie-block)`
- 块级元素：`div  p ul ol li dl dt dd h1 h2 h3 h4 h5 h6  header section aside footer article table thead tbody tr td form   `

## 2、HTML重要属性

- `a`标签的`href`和`target`：href规定链接的URL。target有以下属性：

  ![image](https://user-images.githubusercontent.com/64902360/164011699-0ec71b31-c44a-4162-8ed8-14bd9a77cd12.png)

- `img`标签的`src`和`alt`属性。src规定显示图像的 URL；alt:图片不可用时候，文字显示出来

- `table td`标签的`colspan`和`rowspan`：`colspan`规定单元格可以横跨的列数，`rowspan`规定单元格可以横跨的行数

- `form的target method以及enctype`：target规定表单提交到哪里，method有get和post，规定发送form-data的HTTP方法。enctype:指定编码，如果上传文件指定要用form-data

- `input的type,value`：type有以下属性值，value规定input元素的值。
  ![image](https://user-images.githubusercontent.com/64902360/164011939-6f75848d-82e4-46cb-9a3e-e570a58ad742.png)

- `button的type`：如下所示。
  ![image](https://user-images.githubusercontent.com/64902360/164012034-5c795205-0ef4-4ca9-9e6b-91be00807a7f.png)

- `select的option`：option 元素定义下拉列表中的一个选项（一个条目），它有以下属性：
  ![image](https://user-images.githubusercontent.com/64902360/164012210-aa34685a-02da-417f-8494-9917d4875caf.png)

- `label`：label与input元素进行关联，\<label> 标签为 input 元素定义标注。\<label> 标签的 for 属性应当与相关元素的 id 属性相同。
  ```html
  <form>
    <label for="male">Male</label>
    <input type="radio" name="sex" id="male" />
    <br />
    <label for="female">Female</label>
    <input type="radio" name="sex" id="female" />
  </form>
  ```


## 3、HTML作用

- 对机器友好，有利于SEO
- 开发者友好，增强了可读性，结构更加清晰

## 4、HTML5新增内容

- 新增语义化标签
  - `header`：元素代表 网页 或section的页眉
  - `section`：元素代表文档的 节或者段
  - `article`：标签定义外部的内容
  - `nav`：元素代表页面的导航链接区域。用于定于页面的主要导航部分
  - `aside`：元素被包含在article元素中作为主要内容的附属信息部分;最典型的是侧边栏
  - `footer`：标签定义文档或节的页脚

- 新增视频音频标签

  - `video`：视频标签，常见属性如下

    ![image-20220420095915327](G:\typora插入图片\image-20220420095915327.png)

  - `audio`：音频标签，常见属性如下

    ![image-20220420095955903](G:\typora插入图片\image-20220420095955903.png)

  - 表单增强(新的元素，表单验证)
    - 新的元素：`url、email、number、range、date、month、week、time、datetime、search、tel、color`

  - `Canvas`+`WEBGL`等技术，实现无插件的动画以及图像、图形处理能力
  
  - 本地存储，可实现`offline`应用；
  
  - `websocket`，一改`http`的纯`pull`模型，实现数据推送的梦想；
  
  - MathML，SVG等，支持更加丰富的render

## 5、元素分类

- 默认样式分类

  - 块级元素 (`display: block`)

    特点：1、会独占一行，不管内容的长度；2、块级元素的宽度会自动填满其父元素的宽度；3、可以设置`margin、padding、width、height`。

    元素：`duv p ul  li table form`等

  - 行内元素（`display:inline`）

    特点：1、不会独占一行，会紧跟排列，知道没有空间为止；2、设置width、height无效；3、水平方向上设置`margin、padding`有效，垂直方向上设置无效。

    元素：`a b span  select strong em` 

  - 行内块元素：(`display: inlie-block`)

    特点：具有块级元素的特点，也有行内元素的特点。1、不会独占一行，一行中可以放多个行内块元素，但是之间会有空隙，设置它的上一级font-size为0，才会消除间隙。2、可以设置元素的宽度和高度

    元素：`img input textarea  select buttoon video audio`

- 嵌套关系
  - 块级元素可以包含行内元素
  - 块级元素不一定包含块级元素（p标签不能包含div）
  - 行内元素一般不能包含块级元素

- 默认样式和reset

  HTML标签在浏览器中都有默认的样式，不同的浏览器的默认样式之间存在差别。例如ul默认带有缩进样式，在IE下，它的缩进是由margin实现的，而在Firefox下却是由padding实现的。开发时浏览器的默认样式可能会给我们带来多浏览器兼容性问题，影响开发效率。现在很流行的解决方式是一开始就将浏览器的默认样式全部覆盖掉，这就是css reset。[Normalize.css](http://necolas.github.io/normalize.css/) 只是一个很小的CSS文件，但它在默认的HTML元素样式上提供了跨浏览器的高度一致性。相比于传统的`CSS reset`，`Normalize.css`是一种现代的、为[HTML5](https://so.csdn.net/so/search?q=HTML5&spm=1001.2101.3001.7020)准备的优质替代方案。
