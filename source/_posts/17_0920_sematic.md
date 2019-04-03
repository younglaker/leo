---
layout: post
title:  Semantic UI 及在 React.js 下开发的一些坑
date:   2017-09-20 08:24:00
category: [ React.js]
tags: [JavaScript,HTML5,React.js,Semantic]
---

<!-- ![Semantic][1] -->

<!--more-->

> 欢迎交换友链： [进击的程序媛 http://laker.me/blog/]( http://laker.me/blog )
> Github：[https://github.com/younglaker]( https://github.com/younglaker )
> V信: lakerHQ （请注明‘来自博客’）

最近做了一个 React + Semantic 的电商网站，记录一些坑。之前都是用 Bootstrap，第一次用 Semantic，有些不习惯。

## React 版

https://react.semantic-ui.com/

## 避免弹框表单自动聚焦

弹框表单自动聚焦第一个 input 本来是好事情，但是如果第一个 input 设置了 selection，自动聚焦就会弹出下拉框，会很奇怪，如果是带实时搜索功能就会触发一次无用的搜索造成资源浪费


dropdown 插件有禁止自动聚焦的属性，[参考1][2]，[参考2][3]:
```
$(selector).modal({
    autofocus: false,
}).modal('show');
```

但是我设置了无效。

又根据 [Stack Overflow 的方法][4] 给 input 设置了 tabindex、autofocus，也未果
```
tabindex="-1" autofocus="false"
```

> 在 react 里 tabindex、autofocus 要写成 tabIndex、autoFocus

## 方法一

实在没有办法，只能伪造一个 input，隐藏在界面最前面，但是不能用display:none

```
.hidden-input {
  position: absolute;
  width: 0;
  border: 0;
  background: none;
  z-index: -99;
  top: -1000px;  // 让input离开窗口视觉范围，不然还是会有聚焦的高亮框
}
```

## 方法二

聚焦时不显示下拉列表：
```
$('.ui.dropdown').dropdown(
    showOnFocus: false, // 聚焦时不展开下拉列表
});
```
## 垂直居中

新增全局 css class，给父级添加就好：

```
.align-item-c {
  display: flex;
  align-items: center;
}
```

## CheckBox 让 label 在左边

### 方法一
让 label 左浮动
http://jsbin.com/tewowa/1/edit?css,output
https://stackoverflow.com/questions/25355614/semantic-ui-positioning-labels

```
<div class="ui toggle checkbox custom">
    <input id="privacy" type="checkbox" checked="checked">
    <label for="privacy">Public</label>
</div>


.custom label {
  float: left;
  margin: 0 5px 0;
}
```
方法二：

让 checkbox 右浮动
https://github.com/Semantic-Org/Semantic-UI/issues/1986

```
.ui.toggle.checkbox[class*="right floated"] {
    float: right !important;
    margin-right: 0em !important;
    margin-left: 1em !important;
}
```

### 方法三
把 label 置空（不能删除，否则 CheckBox 也不见），在 div 前面加个 span 或 lable


```
<label for="privacy">Public</label>
<div class="ui toggle checkbox custom">
    <input id="privacy" type="checkbox" checked="checked">
    <label></label>
</div>
```

## 允许多层弹框

```
$(".modal").modal({'allowMultiple': true})
```

## dropdown 里含 checkbox、searchbox
https://jsfiddle.net/jp8xj0wk/2/
```
$('.ui.dropdown').dropdown({
  action: 'nothing'
});
$('.ui.checkbox').checkbox();

<div class="ui basic right labeled dropdown icon button">
  <i class="dropdown icon"></i>
  <span class="ui tiny header">Filter</span>
  <div class="menu">
    <div class="ui icon search input">
      <i class="search icon"></i>
      <input type="text" name="Search" placeholder="Search&hellip;">
    </div>
    <div class="scrolling menu">
      <div class="ui item checkbox" data-value="item1">
        <input type="checkbox" name="item1">
        <label>First item</label>
      </div>
      <div class="ui item checkbox" data-value="item2">
        <input type="checkbox" name="item2">
        <label>Second item</label>
      </div>
    </div>
  </div>
</div>

```

## 设置下拉选择框已选内容，下拉框全选

在编辑内容页面，需要从后台获取数据，把数据展示在input 里

https://jsfiddle.net/dbr26njq/48/
https://codepen.io/monty5811/pen/xVgrzB

HTML
```
<input type="button" id="setValues" value="Set Values" />
<input type="button" id="clearValues" value="Clear Values" />

<div class="ui fluid selection search dropdown multiple">
  <input name="tags" type="hidden">

  <div class="default text">Select</div>
  <i class="dropdown icon"></i>
  <div class="menu">
    <div class="item" data-value="1">Angular</div>
    <div class="item" data-value="2">CSS</div>
    <div class="item" data-value="3">JS</div>
  </div>
</div>

```

JavaScript
```
$('.ui.dropdown').dropdown({
    onChange: function (value, text, $selectedItem) {
      console.log(value);
    },
    forceSelection: false,
    selectOnKeydown: false,
    showOnFocus: false, // 聚焦时不展开下拉列表
    on: "hover"
});


// 清空
$('#clearValues').click(function() {
    $('.ui.dropdown').dropdown("clear");
});

// 全选
$('#setValues').click(function() {
    $('.ui.dropdown').dropdown("set selected", [
        "1","2","3"
    ]);
});
```

单选下拉框的赋值方法一样：
http://jsfiddle.net/0qobkc2x/
```
<select id="test" class="ui dropdown">
    <option value="">Select an option...</option>
    <option value="A">AAA</option>
    <option value="B">BBB</option>
</select>

$('#test').dropdown('set selected','B');

```

## 侧边菜单栏铺满窗口
https://stackoverflow.com/questions/1575141/make-div-100-height-of-browser-window
`height:100%`无效。除了一些老方法，这里采用用视图单位。

单位：
- vh：viewport height
- vw: viewport width
- vmin: viewport minimum length
- vmax: viewport maximum length

例如 1vh = 1% of the viewport的高度

所以可以这样写：
```
div {
    height:100vh;
}
```

可以减去头部高度：

```
height: calc(100vh - 50px);
```

## 与父级同高，等高
方法一:
http://jsfiddle.net/emn13/7FFp3/
```
.parent { display: table; }
.parent > div {display: table-cell; }
```

方法二
http://jsbin.com/hetunujuma/1/edit?html,css,output
```
.parent { display: flex; }
.parent>div { flex:1; }

```

## checkbox 监听
https://stackoverflow.com/questions/27702613/semantic-ui-checkbox-onchange-event-not-triggered
http://jsfiddle.net/mktm/xwp1L695/
https://github.com/Semantic-Org/Semantic-UI/issues/375

checkbox 是用 label 的 before 伪装的，，input 是隐藏的，只能根据父级 div 的 checked 属性来判断

```
var MyCheckBox = React.createClass({
    getInitialState: function() {
        return {
            checked:false
        }
    },

    handleChange: function(event) {
        this.setState({checked: !this.state.checked});
    },

    render: function() {
        return (
            <div className="ui toggle checkbox" onClick={this.handleChange} />
                <input type="checkbox" value={this.state.checked} />
            </div>
        )
    }
});
```

## 时间、日期控件 date range picker

日期范围选择器jQuery：https://github.com/longbill/jquery-date-range-picker
日期范围选择器jQuery：https://codecanyon.net/item/calentim-date-time-range-picker/20099228
很多功能的选择器React：https://github.com/react-component/calendar
小时范围选择器 https://codepen.io/fikrimarhan/pen/Pmaooq
日期、小时范围选择 http://jonthornton.github.io/jquery-timepicker/
小时范围滑块：https://codepen.io/caseymhunt/pen/kertA


  [1]: http://77g54f.com1.z0.glb.clouddn.com/bgt-20170928.png?imageView2/1/q/100|watermark/1/image/aHR0cDovLzc3ZzU0Zi5jb20xLnowLmdsYi5jbG91ZGRuLmNvbS9sYWtlcjEucG5n/dissolve/100/gravity/South/dy/10
  [2]: https://semantic-ui.com/modules/dropdown.html#/settings
  [3]: https://github.com/Semantic-Org/Semantic-UI/issues/2041
  [4]: https://stackoverflow.com/questions/7827004/how-to-avoid-automatic-focus-on-first-input-field-when-popping-a-html-form-as-a


