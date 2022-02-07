# SbPlaceholder Wiki
## 一. 简介

### 这是什么?

SBPlaceholder是一个基于PlaceholderAPI由小明(QQ:1360197420)开发的插件，本插件提供了大量的函数，运算符号等，使PlaceholderAPI的功能更加强大，例如，在特定的情况下显示特定的占位符等。为了使你完全掌握SBPlaceholder的用法，我强烈建议你按照顺序完整的看完本教程。

### 如何调用?

和其他PlaceholderAPI附属插件一样，本插件也有一个标识符，本插件的标识符非常简短：s，这代表这在任何需要用到本插件的时候使用 %s_<表达式>% 即可，表达式何如书写将会在下文详细说明。

### 如何安装？

1. 关闭服务器。
2. 下载前置插件PlaceholderAPI和SBPlaceholder并放入plugins文件夹。
3. 开启服务器。
4. 使用指令 “/papi list”来检测是否安装成功，如果有一个s，说明安装成功。

## 二. 快速上手

### 最简单的表达式

%s_hello% 这个占位符非常浅显易懂，s_是插件的标识符不需要进行观察，作用仅仅是让服务器知道这后面的是一个SBPlaceholder表达式，而后面的hello才是表达式的内容，这就是一串文本，SBPlaceholder会直接将hello返回，你可以使用指令 /papi parse me %s_hello% 来测试。

### 在表达式中进行运算

%s_2+5+1% 你可以注意到这个表达式使用了运算符号”+”，加号的意义是求和，SBPlaceholder会处理像是这样的运算符，你可以在下面的表格中查看所有的数学运算符。理所当然的，这个占位符会返回8。

| 运算符号 | 符号名称 | 优先级 | 示例输入 | 示例输出 |
| -------- | -------- | ------ | -------- | -------- |
| +        | 加       | 20     | 5+3      | 8        |
| -        | 减       | 20     | 6-4      | 2        |
| *        | 乘       | 30     | 7*5      | 35       |
| /        | 除       | 30     | 8/6      | 1.25     |
| ^        | 乘方     | 40     | 2^3      | 8        |
| √        | 开方     | 40     | 2√9      | 3        |

### 在表达式中使用其他占位符

%s_{.player_health.}/2% 这个占位符要求你安装了PlaceholderAPI的另一个拓展player，如果你没有安装的话，你可以使用 /papi ecloud download player来安装，安装结束后记得重载PlaceholderAPI。回到正题，你可以在SBPlaceholder中调用其他拓展的占位符，只需要将此占位符的格式从 %xxx% 改为 {.xxx.} 即可，之后SBPlaceholder会正常的进行运算，返回玩家生命值的一半。

[更新于1.2.0] 你现在可以使用类似papi(player_health)的格式来解析其他占位符，这还支持以其他玩家的立场来解析占位符，详见后文。

### 在表达式中使用漂亮的颜色

在大多数其他插件中，颜色代码的符号都是&，但是在本插件中&的含义是and（具体作用会在下文中讲述），所以本插件的颜色代码符号是@，但你依旧可以使用&，但是需要加上转义符\，也就是\&，转义符的概念请查看下一段落。

### 转义符的概念

在刚刚，我们说到了六个数学运算符，这时候你很可能回想，如果我就想用普通的加号怎么办，我就想让他显示一个加号，我不希望他去求和，这时候就需要用到转义符\\，注意这个斜杠不是普通的斜杠，而是反斜杠，转义符的作用是使下一个文本变为普通的文本，而不是当作运算符，这也就是为什么\&可以当作颜色代码使用的原因。举例：%s_评分: B\\+%，这个表达式会返回“评分: B+”这段文本，但是如果去掉表达式中的转义符，插件就会报错，因为插件无法计算”评分: “和一个空的文本的和。

## 三. 全部运算符

上文中，我们展示了所有的数学运算符，他可以帮助你计算一些数学问题，但是本插件的运算符远不止如此，接下来你会看到本插件所有的运算符。每个运算符都具有一个优先级，所有运算符会按照优先级从低到高的顺序进行运算。

### 条件运算符

条件运算符可以更具你给出的前后的内容进行判断，如果满足条件，就会返回true，否则返回false。

| 运算符号 | 符号名称 | 优先级 | 示例输入 | 示例输出 |
| -------- | -------- | ------ | -------- | -------- |
| >        | 大于     | 10     | 10>3     | true     |
| <        | 小于     | 10     | 10<3     | false    |
| =        | 等于     | 10     | hi=hello | false    |

 

### 逻辑运算符

逻辑运算符只有两个，他们都基于true和false，并且运算符会在两端都为true的情况下返回true，而或者运算符只要有一个是true就会返回true，否则都是返回false。

| 运算符号 | 符号名称 | 优先级 | 示例输入    | 示例输出 |
| -------- | -------- | ------ | ----------- | -------- |
| &        | 并且     | 5      | true&false  | false    |
| \|       | 或者     | 5      | True\|false | true     |

### 文本运算符

文本运算符拥有一个最低的优先级0，这意味着他会在所有其他运算符运算完毕后处理，正如其名，他会连接他两端的文本。

| 运算符号 | 符号名称 | 优先级 | 示例输入 | 示例输出 |
| -------- | -------- | ------ | -------- | -------- |
| #        | 连接     | 0      | Is  #3+5 | Is  8    |

### 运算符总览

虽然每个符号都有自己的优先级，但你可以使用小括号来自由的控制运算流程。例如：%s_答案是: #3*(2+3)% 返回“答案是: 15”。

| 运算符号 | 符号名称 | 优先级 | 示例输入               | 示例输出 |
| -------- | -------- | ------ | ---------------------- | -------- |
| #        | 连接     | 0      | Is  #3+5               | Is  8    |
| &        | 并且     | 5      | true&false             | false    |
| \|       | 或者     | 5      | True\|false            | true     |
| >        | 大于     | 10     | 10>3                   | true     |
| <        | 小于     | 10     | 10<3                   | false    |
| =        | 等于     | 10     | hi=hello               | false    |
| +        | 加       | 20     | 5+3                    | 8        |
| -        | 减       | 20     | 6-4                    | 2        |
| *        | 乘       | 30     | 7*5                    | 35       |
| /        | 除       | 30     | 8/6                    | 1.25     |
| ^        | 乘方     | 40     | 2^3                    | 8        |
| √        | 开方     | 40     | 2√9                    | 3        |
| (  )     | 括号     | ∞      | 括号内的表达式优先计算 |          |

## 函数的使用

### 什么是函数?

函数是本插件最为强大的功能，利用函数你可以写出一些惊人的占位符。所有函数的格式都是 函数名(参数1,参数2,参数3···)，但不同的函数需要的参数不同，当你在占位符中使用一个函数，插件会自动将其解析并返回解析后的结果，函数不能和普通的表达式连用，必须使用文本连接符#来连接他们。本章节会详细的向你介绍所有函数的使用方法、需要的参数等信息。

### 函数列表

- **getAuthor()**

  返回插件作者的名字，可以用于调试。

  ```
  %s_getAuthor()%
  > xming_jun
  ```

- **slice(原文本, 起始位置, 结束位置)**

  返回原文本从起始位置开始至结束位置的文本。

  ```
  %s_slice(hello there I am xm,2,9)%
  > ello the
  ```

- **repeat(原文本, 重复次数, [存储变量])**

  将原文本重复一定次数然后返回。
  如果使用第三个参数, 则每次重复时都会先将当前循环次数作为变量传入原文本内。

  ```
  %s_repeat(3,6)%
  > 333333
  ```

  ```
  # 重复五次, 每次都将变量i设置为当前的循环次数。
  %s_repeat([i],5,i)%
  > 12345
  ```

  ```
  %s_repeat(if([i]>9,X,[i]),12,i)%
  > 123456789XXX
  ```

- **mod(被除数, 除数)**

  返回第一个参数除第二个参数后的余数。

  ```
  %s_mod(19,4)%
  > 3
  ```

- **round(原数字, 保留小数位数)**

  返回将原数字四舍五入并保留指定的小数位数。

  ```
  %s_round(3.1415926,3)%
  > 3.142
  ```

- **if(true/false, 如果true, 如果false)**

  如果参数1的数是true, 就返回第一个参数, 否则返回第二个参数。

  ```
  # if的第一个参数用到了条件运算符，插件会自动解析成true，因为是true所以返回参数二，也就是1。
  %s_if(5>3,1,2)%
  > 1
  ```

- **len(任意文本) <sup>[v1.0.1]</sup>**

  返回唯一参数的文本长度。

  ```
  %s_len(hello world)%
  > 11
  ```

- **abs(任意文本) <sup>[v1.0.1]</sup>**

  返回唯一参数的绝对值。

  ```
  %s_abs(-6)%
  > 6
  ```

- **max(数1,文本1,数2,文本2......) <sup>[v1.0.1]</sup>**

  函数介绍：参数需要成对出现，返回所有奇数位中最大的那个对应的文本。

  ```
  %s_max(3,三最大,5,五最大,1,一最大)%
  > 五最大
  ```

- **min(数1,文本1,数2,文本2......) <sup>[v1.0.1]</sup>**

  函数介绍：同max, 只不过是最小

  ```
  %s_min(3,三最小,5,五最小,1,一最小)%
  > 一最小
  ```

- **time() <sup>[v1.0.2]</sup>**

  获取当前的毫秒级时间戳

  ```
  %s_time()%
  > 1606316883659
  ```

- **timeformat(转换格式, 时间戳) <sup>[v1.0.2]</sup>**

  函数介绍：将时间戳转换为便于阅读的格式，两个参数均可空，如果参数1为空则默认使用”yyyy\\-MM\\-dd HH:mm:ss”，如果第二个参数为空则默认使用当前时间戳。注意：在转换格式中你很可能需要用到转义符，如果你不知道转义符是什么请阅读前文。

  ```
  %s_timeformat()%
  > 2020-11-25 23:01:35
  ```

  ```
  %s_timeformat(yyyy MM dd HH mm:ss)%
  > 1970 01 01 08 00 00
  ```

  ```
  %s_timeformat(yyyy MM dd HH mm ss,123456789)%
  > 1970 01 02 18 17 36
  ```

  在转换格式中你不仅可以使用默认格式中的这些，还有这些：

  | 格式 | 描述                     |
  | ---- | ------------------------ |
  | G    | 年代标识符               |
  | y    | 年份                     |
  | M    | 月份                     |
  | d    | 日期                     |
  | h    | 十二时制的小时（1-12）   |
  | H    | 二十四时制的小时（0-23） |
  | m    | 分钟                     |
  | s    | 秒钟                     |
  | S    | 毫秒                     |
  | E    | 星期几                   |
  | D    | 今年的第几天             |
  | F    | 一个月中的第几个星期几   |
  | w    | 一年中的第几个星期       |
  | W    | 一月中的第几个星期几     |
  | a    | 上午/下午                |
  | k    | 二十四时制的小时（1-24） |
  | K    | 十二时制的小时（0-11）   |
  | z    | 时区                     |

- **papi(任意文本) <sup>[v1.2.0]</sup>**

  解析其他占位符，并且在插件版本1.3.1后可以在占位符后使用 **as [目标名]** 的格式来解析其他玩家的占位符。
  该函数比较特殊，你可以任意的在函数的唯一参数中使用逗号且永远只有一个参数。

  ```
  # 获取玩家自己的等级
  %s_papi(player_level)%
  > 20
  ```

  ```
  # 获取玩家xming_jun的等级
  %s_papi(player_level as xming_jun)%
  > 100 
  ```

- **c(常量名,常量参数1,常量参数2……) <sup>[v1.2.0]</sup>**

  一项重复的功能为了可以方便的调用，SbPlaceholder提供常量功能，你可以在config.yml中配置常量，然后使用本函数方便的调用。

  ```
  # 调用配置文件中的halfHealth常量
  %s_c(halfHealth)%
  > 10
  ```

  ```
  # 调用配置文件中的numberList常量，并将5作为参数传入。
  %s_c(numberList,5)%
  > 1 2 3 4 5
  ```

- **foreach(变量名, 源文本, 新文本, [分割符], [新分隔符]) <sup>[v1.3.0]</sup>**

  对源文本进行分隔, 然后逐个处理每个源文本。

  分隔符默认为空格，新分隔符默认等同于分隔符。

  ```
  # 调用配置文件中的halfHealth常量
  %s_c(halfHealth)%
  > 10
  ```

  ```
  # 调用配置文件中的numberList常量，并将5作为参数传入。
  %s_c(numberList,5)%
  > 1 2 3 4 5
  ```

- **random([最小值], [最大值]) <sup>[v1.3.0]</sup>**

  获取一个0-1的随机小数，如果同时给出两个参数，则改为从第一参数到第二参数范围内的全部整数。

  ```
  %s_random()%
  > 0.653986943523
  ```

  ```
  # 调用配置文件中的numberList常量，并将5作为参数传入。
  %s_random(10,100)%
  > 34
  ```

## 五. 插件运用示例

### 1. 检测玩家血量并判断是否死亡

```
%s_if(papi(player_health)>0,papi(player_health),Dead)%
```

这个占位符会判断玩家的生命值是否为0，如果不为0，就会返回玩家的生命值，否则就返回Dead。

### 2. 检测玩家血量并漂亮的画出来

```
%s_repeat(@ci,papi(player_health)*1)#repeat(@7i,20-papi(player_health))#@8]%
```

这个占位符会更具玩家当前的生命值画出一个漂亮的文本，图片中的i或是两侧的方括号或是颜色都可以自由的任意更改。

![exHealth1](https://user-images.githubusercontent.com/59652585/152693988-26d787d4-7128-402f-9ba8-4db57df25614.png)
![exHealth2](https://user-images.githubusercontent.com/59652585/152693991-a67e203f-2cb2-4f95-b8ac-f4464e2b65c8.png)


### 3. 获取所有在线玩家的生命值

```
%s_foreach(var,papi(playerlist_all,normal,yes,list),papi(player_health as [var]))%
```

这个占位符会获取所有在线玩家的生命值, 并以空格隔开。

注意，使用这个占位符需要安装 Player List 与 Player 拓展。

  
