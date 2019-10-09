# 一、常见不好习惯
##  1.通配符`reset`的问题
```CSS
{padding: 0,margin: 0;}
```
* 容易资源浪费，因为有padding的默认值很少，并不必要
* 对于某些元素，默认`margin`属性是有作用的，比如表单元素在复选框和单选框，用通配符重置后，会挤成一团

##  2.容器定高在问题
* 在开发时候，容器被定死高度，但是在之后不能保证需求不变，如果要添加新条目在时候，布局容易出现bug，会降低容错率和维护性

##  3.50%的问题
```css
dt, dd{
    width: 50%;
}
dt{
    float: left;
}
dd{
    float: right;
    text-align: right;
}
```
* 这种布局在实际开发容易有局限，比如在移动端，只有300多像素，布局在文字容易掉出
* 比较好在方法：左侧安全宽度，右侧自动分配剩余空间

##  4.absolute实现问题
```css
dl {
  border: 1px solid #000;
  position: relative;
}
dd {
  position: absolute;
  right: 0;
  margin: -1.2em 0 0 0;
}
```

##  5.relative实现的问题
```css
dd {
  position: relative;
  top: -20px;
}
```
最大的问题在于`relative`元素定位的时候原本占据的空间他是依然保留的，<br>
于是会留下一片空白区域。这里可以把`top`改成`margin-top`效果就可以了

##  6.左右浮动的问题
原代码：
```css
dt{
    float: left;
    clear: left;
}
dd{
    float: right;
    clear: right;
}
```

修改后:
```css
dt{
    float: left;
    clear: both;
}
dd{
    float: right;
}
```
因为，根据张老师的《CSS世界》解释，`clear:left`和`clear:right`，直接用`clear:both`代替

# 二、良好在实现
##  1.这个案例的良好布局
左侧固定宽度，宽度足够安全，右侧自动填满剩余空间<br>
左侧dt标签空间设置为`5em`,单位不是'px','rem'<br>
优点：无论容器大小，左侧不会空间不足，容错性强

##  2.dt标签绝对定位
```CSS
dt  { position: absolute; }
dd  { text-align: right;  margin-left:  5em;  }
```
### 优点：
* 兼容性好，低版本IE浏览器支持<br>
### 缺点：
* `position: absolute`元素，如果布局复杂，会出现元素层叠

##  3.Flex布局
```CSS
dl {
    display: flex;
    flex-wrap: wrap;
}
dt {
    width: 5em;
}
dd {
    width: calc(100% - 5em);
    text-align: right;
}
```

### 优点：
  布局的呈现容易好理解。
### 缺点：
  不足就是会存在些许兼容性问题，在一些老旧的Android手机上。
  
##  4.Grid布局
```CSS
dl {
    display: grid;
    grid-template-columns: auto 1fr;
    grid-column-gap: 1em;
}
dd {
    text-align: right;
}
```
### 优点：
  容错率最强
  
##  5.float浮动实现
```CSS
dt {
    width: 5em;
    float: left;    
}
dd {
    text-align: right;
    overflow: hidden;    
}
```
### 优点：
  关键`overflow: hidden`，文字内容再多也不会浮动环绕<br>
  兼容性：直到E7浏览器灰支持，IE6不支持
  
##  6.借助原生流体特性实现
```CSS
dd {
    margin: -1.5em 0 0 5em;
    text-align: right;    
}
```
### 优点：
  兼容性最强，IE6也支持，代码量最少
  
##总结
* 以上五种代码的-demo地址[demo](https://www.zhangxinxu.com/study/201901/css-quiz-1-layout-demo.php)
* 更详细的内容-[鑫空间](https://www.zhangxinxu.com/wordpress/2019/01/css-quiz-1/)
  
