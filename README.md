# JavaScript i18n

**请先下载示例代码，确认运行没有问题再运用到你的项目中。**

由于实现原理，本项目存在无法克服的一个小缺陷，就是当默认设为非原生文本时，会先显示原生文本而后很快转变为目标语言文本。
- Example1 是本项目的最初版本，只支持双语切换。
- Example2 则支持无限多种语言，可被视为升级版。

用法介绍基于 Example2，两者基本原理相同。

## HTML 改动

### 多语言切换按钮组

首先，你需要一个用于语言切换的按钮组：

```
<div id="languageSwitcher">
    <a id="buttonZh" href="javascript:;">中</a>
    |
    <a id="buttonEn" href="javascript:;">EN</a>
    |
    <a id="buttonJp" href="javascript:;">日</a>
</div>
```

`languageSwitcher` 能够方便为切换按钮组添加 CSS 样式，与 JavaScript 无关。

`buttonZh` 和 `buttonEn` 等则是 JavaScript 所需的，如要修改，请一并修改。

### 多语言文本类

其次，你需要为所有需要做多语切换的文本套上一层：

```
<span class="keys">
    需要多语切换的文本
</span>
```

`keys` 是 JavaScript 调用所需的，如要修改，请一并修改。

至此，HTML 部分的修改完成。

## JavaScript 改动

```
function htmlTitleSwitcher(){
    if(ls.lang == "zh"){
        document.title = "示例网页";
    }else if(ls.lang == "en"){
        document.title = "Example Website";
    } else if (ls.lang == "jp") {
        document.title = "ウェブサイトの例";
    };
}
```

这部分定义了双语的网页标题，也就是显示在浏览器标签上的文本，请按需改动。所有你需要修改的只有 `document.title = ` 后边的字符串。

之后就是用于中文转换外语的：

```
for(i=0; i<keys.length; i++){
    replace("这是一行用于演示的文本。", "This is an example line of text.");
}
```

你只需要把 `这是一行用于演示的文本。` 和 `This is an example line of text.` 对应替换成你所需的中外文本即可。

如果你有多处，就换行，再添加一行同样结构的代码就行，比如：

```
replace("甲", "A");
replace("乙", "B");
……
replace("癸", "J");
```

有多少段文本，就整多少行，所以请注意节制。

## 新版特性

变更一下实现思路就实现了多语切换，不错不错。

如果是做成语言两两互切（比如中-英，英-日，日-中），代码会很冗余很傻（几何级增长），所以可以在切换时，令语言初始化（回归到中），然后基于中文变换为其他语言，这样只需要做单向 replace 方法就能达成目标，只是会需要更多的刷新，但这点不便应该无所谓。

## 后记

关于本项目开发的故事，请见我的博文 [纯 JavaScript 双语化小记](https://zexwoo.blog/pure_js_bilingualism/)。