# JavaScript i18n

**请先下载示例代码，确认运行没有问题再运用到你的项目中。**

由于实现原理，本项目存在无法克服的一个小缺陷，就是当默认设为非原生文本时，会先显示原生文本而后很快转变为目标语言文本。
- Example1 是本项目的最初版本，只支持双语切换。
- Example2 则支持无限多种语言，可被视为升级版。

## HTML 改动

### 双语切换按钮组

首先，你需要一个用于语言切换的按钮组：

```
<div id="languageSwitcher">
    <a id="buttonZh" href="javascript:;">中</a>
    /
    <a id="buttonEn" href="javascript:;">EN</a>
</div>
```

`languageSwitcher` 能够方便为切换按钮组添加 CSS 样式，与 JavaScript 无关。

`buttonZh` 和 `buttonEn` 则是 JavaScript 所需的，如要修改，请一并修改。

### 双语文本类

其次，你需要为所有需要双语切换的文本套上一层：

```
<span class="keys">
    需要双语切换的文本
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
    };
}
```

这部分定义了双语的网页标题，也就是显示在浏览器标签上的文本，请按需改动。所有你需要修改的只有 `示例网页` 和 `Example Website` 这两部分。

之后就是主要文本：

```
for(i=0; i<keys.length; i++){
    replace("This is an example line of text.", "这是一行用于演示的文本。");
};
```

还有用于中转英的：

```
for(i=0; i<keys.length; i++){
    replace("这是一行用于演示的文本。", "This is an example line of text.");
}
```

你只需要把 `这是一行用于演示的文本。` 和 `This is an example line of text.` 对应替换成你所需的中英文本即可。

如果你有多处，就换行，再添加一行同样结构的代码就行，比如：

```
replace("This is an example line of text.", "这是一行用于演示的文本。");
replace("This is an example line of text. 2", "这是一行用于演示的文本。2");
```

有多少段文本，就整多少行，所以请注意节制。

## 展望

变更一下实现思路，其实可以实现多语切换。

如果是做成语言两两互切（比如中-英，英-日，日-中），代码会很冗余很傻（几何级增长），所以可以在切换时，令语言初始化（回归到中），然后基于中文变换为其他语言，这样只需要做单向 replace 方法就能达成目标，只是会需要更多的刷新，但这点不便应该无所谓。

确实实现了。双语切换请用 Example1 文件组；多语切换请用 Example2 文件组，原理相同，修改也都方便。

## 后记

关于本项目开发的故事，请见我的博文 [纯 JavaScript 双语化小记](https://zexwoo.blog/pure_js_bilingualism/)。