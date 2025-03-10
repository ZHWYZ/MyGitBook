
## 1.前言
Markdown的原生语法是不支持绘制流程图的，但是可以通过Mermaid插件来实现，该插件可以绘制常用的 “流程图”、“时序图”、“类图”、“状态图”、“甘特图”、“饼图” 等，下面将重点介绍如何通过Mermaid 绘制流程图。

## 2.基本用法
基本的流程图包含：流程图布局方向、几何图形和连接线三个部分组成。

```
graph TD;
	A[节点A] --> B[节点B];
    B --> C(节点C);
```
使用mermaid后显示效果如下：
```mermaid
graph TD;
	A[节点A] --> B[节点B];
    B --> C(节点C);
```
- `graph TD` 表示绘制从上到下的流程图，graph表示流程图的开始，TD 代表 "Top to Down"。
- `A --> B` 表示从节点A指向节点B。
- 节点的内容用方括号 `[]` 表示，形状可以是矩形 `[节点]` 或者是圆角矩形 `(节点)`。
 
## 3.详细用法

### 3.1箭头方向
可以使用不同的方向控制流程图的布局方式：
- `TD`：从上到下 (Top to Down)
- `LR`：从左到右 (Left to Right)
- `BT`：从下到上 (Bottom to Top)
- `RL`：从右到左 (Right to Left)

### 3.2节点形状
采用的节点形状有如下几种
1. 默认节点 A
2. 文本节点 B[bname]
3. 圆角节点 C(cname)
4. 圆形节点 D((dname))
5. 非对称节点 E>ename]
6. 菱形节点 F{fname}
```mermaid
graph TD;
  A
  B[bname]
  C(cname)
  D((dname))
  E>ename]
  F{fname}
```

### 3.3连接线的形状
常用的节点间的连接线有多种形状，而且可以在连接线中加入标签：

```
1.箭头连接 A1-->B1
2.开放连接 A2---B2
3.标签连接 A3--text---B3 或者 A3---|text|B3
4.箭头标签连接 A4--text-->B4 或者 A4-->|text|B4
5.虚线开放连接 A5.-B5
6.虚线箭头连接 A6-.->B6
7.标签虚线连接 A7-.text.-B7
8.标签虚线箭头连接 A8-.text.->B8
9.粗线箭头连接 A10==>B10
```


```mermaid
graph TB;
	A1-->B1;
	A2---B2;
	A3--text---B3;
	A3---|text|B3;
	A4--text-->B4;
	A4-->|text|B4;
```

```mermaid
graph TB;
	A5-.-B5;
	A6-.->B6;
	A7-.text.-B7;
	A8-.text.->B8;
	A9==>B9;
```


### 3.4定义元素
|元素类型|代表意义|形状|
|---|---|---|
|start|开始|圆角矩形|
|end|结束/完成|圆角矩形|
|operation|流程操作|普通矩形|
|subroutine|预定子流程|双边线矩形|
|condition|条件判断|菱形|
|inputoutput|输入输出|平行四边形|
例子如下：
```
graph TD;
    start((开始)) --> input[/输入账号密码/]
    input --> check{验证格式}
    check -- 格式正确 --> auth[调用鉴权接口]
    check -- 格式错误 --> error[/提示输入错误/]
    auth --> cond{是否通过?}
	cond -- 是 --> 通过
	subgraph 通过
        update[更新登录状态]
        log[/记录日志/]
    end
    cond -- 否 --> error
    update --> finish((结束));
    log --> finish;
```

```mermaid
graph TD;
    start((开始)) --> input[/输入账号密码/]
    input --> check{验证格式}
    check -- 格式正确 --> auth[调用鉴权接口]
    check -- 格式错误 --> error[/提示输入错误/]
    auth --> cond{是否通过?}
	cond -- 是 --> 通过
	subgraph 通过
        update[更新登录状态]
        log[/记录日志/]
    end
    cond -- 否 --> error
    update --> finish((结束));
    log --> finish;
```

## 4.自定义节点样式
