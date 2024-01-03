# FlyingSacuer + Freemarker生成PDF 

[·Freemarker简单语法使用](#·Freemarker简单语法使用)

​	[一、 宏](#一、 宏)

​	[二、函数](二、函数)

​	[三、判断](#三、判断)

​	[四、循环](#四、循环)

​	[五、变量](#五、变量)

***

***

## ·Freemarker简单语法使用

### 一、 宏

#### 1、定义一个macro

直接在head标签中定义

```html
<head>
    <#macro macroName macroParam>
        <h1>hello ${param}</h1>
	</#macro>
</head>
```

定义到ftl文件中，通过<#include "路径"/>引用

```html
<head>
	<#include "test.ftl"/>
</head>
```

#### 2、通过@使用macro。

```html
<body>
	<@macroName "world"/>
</body>
```

#### 3、解析后的效果。

```html
<body>
	<h1>hello world</h1>
</body>
```



***



### 二、函数

#### 1、定义一个function

```html
<head>
    <!-- 同样可以使用引用文件的方式，与宏类似 -->
    <#function functionName functionParam>
        <!-- 使用<#return>标签返回函数的返回值 -->
        <#return " " + functionParam/>
	</#function>
</head>
```

#### 2、在freemark标签中直接调用function。

macroName就是上面定义的宏 

```html
<body>
    <!-- 在${}中间写入要使用的函数 -->
	<h1>hello${functionname("world")}</h1>
</body>
```

#### 3、解析后的效果。

```html
<body>
	<h1>hello world</h1>
</body>
```

#### 4、注意

4-1、函数没有返回值，调用后



***



### 三、变量

#### 1、普通变量

1-1、定义变量

```html
<head>
	<#assign globalArray = ['helo', ' ', 'world']/>
</head>
```

1-2、 使用

```html
<body>
    <#list globalArray as item>
        <!-- 在${}中间写入要使用的变量 -->
        ${item}
    </#list>
</body>
```

1-3、解析后的效果

```html
<body>
    hello world
</body>
```



#### 2、局部变量

2-1、定义一个函数，在函数中定义局部变量并返回

```html
<#function localMethod>
    <!-- 通过#local标签定义一个变量localVar并赋值为hello world -->
    <#local localVar = "hello world"/>
    <!-- 通过#return标签返回局部变量 -->
    <#return localVar/>
</#function>
```

1-2、 使用函数获取定义的局部变量

```html
<body>
    ${localMethod()}
</body>
```

1-3、解析后的效果

```html
<body>
    hello world
</body>
```

1-4、注意

**local定义的时候，#local标签必须放到<#function>标签或者是<#macro>标签中。否则会报错**



***

### 四、判断

#### 1、通过<#if  表达式>进行判断

```html
<head>
    <#function functionName functionParam>
        <#if "World" = functionParam>
            <!-- if成立的情况 -->
            <#return " " + functionParam/>
        <#elseif "" = functionParam>'
            <!-- elseif成立的情况 elseif中间没有空格 必须放在<#if></#if>标签中间 -->
            <#return " Empty String"/>
        <#else>
            <!-- else的情况 必须放在<#if></#if>标签中间 -->
            <#return " Other"/>
        </#if>
	</#function>
</head>
<body>
	<@macroName functionname("world")/>
    <@macroName functionname("")/>
    <@macroName functionname("hello")/>
</body>
```

#### 2、解析后的效果

```html
<body>
	<h1>hello world</h1>
	<h1>hello Empty String</h1>
	<h1>hello Other</h1>
</body>
```



***



### 五、循环

#### 1、集合或者数组的便利

1-1、比如有一个数据array，其中的值为[1, 2, 3, 4]

```html
<body>
    <#list array as item>
        <h1>item</h1>
    </#list>
</body>
```

1-2、解析后的效果

```html
<body>
    <h1>1</h1>
    <h1>2</h1>
    <h1>3</h1>
    <h1>4</h1>
</body>
```

#### 2、 指定循环的次数

2-1、还是使用array，其中的值为[1, 2, 3, 4]

```html
<body>
    <#list 0..3 as i>
        <h1>array[i]</h1>
    </#list>
</body>
```

2-2、解析后的效果

```html
<body>
    <h1>1</h1>
    <h1>2</h1>
    <h1>3</h1>
    <h1>4</h1>
</body>
```



***



***



### 六、
