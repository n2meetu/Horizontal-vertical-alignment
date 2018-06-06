# Horizontal-vertical-alignment
Horizontal vertical alignment水平垂直居中的实现方式
### 1.Flexbox布局：

```
display:flex;
justify-content:center;
align-items:center;
width:100%;
```

## 2.Bootstrap栅格布局
一共12格，分成3块，每块占4列。居中的内容写在中间的那一块。

## 3.圣杯/双飞翼（水平自适应居中的基础上）
### 第一步：居中的div写在最前面，`width:100%`撑满一整行。三个div都向左浮动`float:left;`
```
<div class="main">Main</div>
<div class="left">Left</div>
<div class="right">Right</div>
```

### 第二步：让三个div显示在同一行

```
div.left { marin-left:100%}
div.right{ marin-left:自身的宽度}
```

### 第三步：让中间的div能够自适应
#### 圣杯布局的做法：
```
div.main{
    padding-left:左div的宽度；
    padding-right:右div的宽度；
}
```
#### 双飞翼布局的做法：
在`div.main`内部再添加一个`div.mc`：
然后设置div.mc的`margin`值

```
margin-left:左div的宽度；
margin-right:右div的宽度；
```
现在，水平居中已经实现了；

#### 第四步：垂直居中
![](http://ozfuwp2os.bkt.clouddn.com/15281892087750.jpg)
在`div.left,div.right,div.main`外面再加一个`div.wrap`,
然后对`div.con`设置 `display:table`,对`div.wrap`设置 

```
display:table-cell;
vertical-align:middle;
```

## 4.relative/positive + top/left+tarnsform
#### 父元素：
`position:relative `
#### 子元素：
```
position:absolute;
top:50%;
left:50%;
transform: translate(-50%, -50%); 
``` 
transform: translate(-50%, -50%);意思是向右移动**自身**50%的宽度，向下移动**自身**50%的高度。

#### 为什么有了`top:50%;left:50%`还要 ` transform: translate(-50%, -50%); `
最初：
![-w285](http://ozfuwp2os.bkt.clouddn.com/15282012362318.jpg)

加了`top:50%;left:50%`后：
![-w341](http://ozfuwp2os.bkt.clouddn.com/15282012410159.jpg)

还需要再往左、往上挪一挪：
![-w555](http://ozfuwp2os.bkt.clouddn.com/15282013387771.jpg)


## 5.relative/positive + top/left+left + margin

和方法4一样，用top和left挪到中间：
![-w341](http://ozfuwp2os.bkt.clouddn.com/15282012410159.jpg)

这之后用` margin-left `和` margin-right `进行处理：

#### 先给`div.child`设置宽度，然后设置`margin`：

![](http://ozfuwp2os.bkt.clouddn.com/15282019903551.jpg)

## 6.用`top,left,bottom,right`
![](http://ozfuwp2os.bkt.clouddn.com/15282022873509.jpg)

**计算公式：**
### top + div.child 的 height +bottom = div.parent 的 height

### left + div.child 的 width +right = div.parent 的 width

如果子元素是行内元素，如`<p>`,要注意一开始就要去掉margin和padding

方法4、5、6有demo……
