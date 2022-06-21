# Lessz

Provide some common less tool functions

## Loops
### Simple keyframes
```less
@import "lessfun/loop.less";
@keyframes frameName {
    .keyframe-loop(1, {
        transform: translate3d(0, 0, 0);
    });
}
```
```less
// 上面👆结果
@keyframe frameName {
    0% {
        transform: translate3d(0, 0, 0);
    }
    100% {
        transform: translate3d(0, 0, 0);
    }
}
```
**参数定义**
```bash
.keyframe-loop(@length, @customCSSBlock: {}, @start: 0, @step: 1);
```
| API  |  解释 | 备注  | 变量名 
|---|---|---| ---|
| @length  | 最大边界  | 从0开始, 传1会得到 0% 和 100%  | @end 
| @customCSSBlock  | 自定义的代码块(和CSS写法相同)  | 不可以传递一个class名或ID名  | @impl 
| @start  | 从哪一个开始  | 默认从1开始(代表元素位置，从1开始)  | @start |
| @step  | 每次的增量  | 默认为1  | @step 

**特殊环境变量**

由于customCSSBlock执行时机的原因, 你可以在block里面使用环境中提供的变量名(即是上方API中的变量名)，如:
```less
@import "lessfun/loop.less";
@keyframes frameName {
    .keyframe-loop(2, @impl: {
        width: @keyframe;
        border: @start solid red;
    });
}
```
```less
// 解析结果
@keyframes frameName {
  0% {
    width: 0%;
    border: 0 solid red;
  }
  50% {
    width: 50%;
    border: 1 solid red;
  }
  100% {
    width: 100%;
    border: 2 solid red;
  }
}
```

### Loop Collections
你可以传递一个Collections用于快速生成CSS定义
```less
@import "lessz/loop.less";

@colors: green, red, blue;
.text {
    .loop-collections(@colors, {
        color: @item;
    });
}
```
```less
// 结果
.test-blue {
  color: blue;
}
.test-red {
  color: red;
}
.test-green {
  color: green;
}
```
**参数定义**
```bash
.loop-collections(@collections, @impl: {})
```
| API  |  解释 | 备注  | 变量名 
|---|---|---| ---|
| @collections  | 所有的集合, 使用逗号分隔  |   | @collections 
| @customCSSBlock  | 自定义的代码块(和CSS写法相同)  | 不可以传递一个class名或ID名  | @impl

**特殊变量名**
| 变量名  |  解释 | 备注 
|---|---|---|
| @index | 下标 | 从0开始 |
| @item | 每一项的值 | 

## Math

## Other
