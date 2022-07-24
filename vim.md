# 第二天
## 1、移动命令
### 移动到行首：
- 数字 0
- ^ 移动到本行第一个不是 blank 字符的位置
### 移动到行尾
- $ 
- g_ 移动到本行最后一个不是 blank 字符的位置
 
由于 ^ 和 g_ 不是很好操作，因此我们需要在 vscode 中做映射
```json
// settings.json 
"vim.normalModeKeyBindings": [
        {
            "before":["H"],

            "after":["^"]
        },
        {
            "before":["L"],
            "after":["g","_"]
        }
    ],
```

## 2、 插入命令
### 插入到行首
- 大写的 I
- shit + h + i
### 插入到行尾
- 大写的 A 
- shit + l + a
### 插入到本行之前
大写的字母 O
## 插入到本行之后
小写的字母 o
## 3、 复制、粘贴、剪切行 命令
复制：yy
粘贴：p
剪切：dd
# 第三天
## 3.1、vim 语法 
```json
// settings.json
"vim.operatorPendingModeKeyBindings": [
        {
            "before":["H"],
            "after":["^"]
        },
        {
            "before":["L"],
            "after":["g","_"]
        }
    ],
```
操作（operation）: 需要配合其他按键去配合这个命令
在 normal 模式下，可以按以下按键，去配合动词，达到想要实现的效果。
在 normal 模式下，判断依据是以 光标闪动地方前面空隙为起点。
- d 删除。配合 数字0删除到行头，字母 h 删除前一个，字母 l 删除后一个，字母 j 和 k 分别 删除 当前行、后一行 和 当前行、前一行，字母 H、L 删除到行头和行尾。
- c 删除并 insert。使用方法和 d 是类似的。
- y 复制。使用方法和 d 类似
- e 移动到下一个单词或者符号末尾（从左往右走）
- w 移动到下一个单词或者符号开头（从左往右走）
- b 移动到上一个单词或者符号开头（从右往左走）
- ge 移动到上一个单词或者符号末尾（从右往左走）
常用组合 删除一个单词 de ，删除一行 dL 等
# 第四天
## 4.1 单个字符相关操作
删除光标所在字符：x
删除光标所在的前一个字符：X
删除当前光标的字符并且进入insert模式：s
[删除光标所在行并且进入insert模式：S]
替换光标所在字符：r
替换光标之后的字符串：R
撤销：u
还原撤销：ctrl + r

# 第五天
## 5.1 可视化模式
基于字符：小写的 v
基于行的：大写的 V
基于块的：ctrl + v
常用组合：选中单词 ve，选中行 V
## 5.2 退出可视化模式
esc、ctrl + \[
## 5.3 导航
搭配动作范围：ve 选中单词，V 选中行
o -> 切换可视区的光标位置（重点）
gv -> 选中上一次选中的可视化模块
## 5.4 组合使用 
即 选中的范围 + 操作符
比如 v + e ，v + y , v+c，ved
# 第六天
## 6.1 操作文本对象
内部对象：v(操作，比如说 c、d、y等) + i + 符号(比如说 单引号、双引号、小括号、大括号等)、这样就能选中指定符号内的内容（不包括 符号 ）。
外部对象：v(操作，比如说 c、d、y等) + a + 符号(比如说 单引号、双引号、小括号、大括号等)、这样就能选中指定符号内的内容（包括 符号 ）。

常用组合举例
- d + i + ( 删除小括号里面的数据
- d + i + b 删除小括号里面的数据
- d + a + b 删除包括小括号在内的数据
- d + i + B 删除花括号里面的数据
- d + a + B 删除包括花括号在内的数据
- v + i + w  选中一个单词
- v + i + \[ 选中中括号内的内容
- d + i + { 删除大括号内的内容
- d + i/a + < 删除 不包括/包括 尖括号的内容
- v + i + t 选中 xml 标签
- v + i/a + \`/\'/\" 选中响应符号中的内容
- v + i + s 选中句子（在 vim 中，只有以 .!? 结尾的才会被当成是一个句子）
- v + i + p 选中段落 
## 6.2 vscode自身集成的 vim 命令
### 6.2.1 vim-textobj-arguments
针对 参数 的（如：function A(a,b,c)），直接使用 
- v + i/a + a（这个 a 代表 arguments 参数的意思） 表示选中光标所在参数，i 只选中参数，a 的话就会包含前面那个逗号
### 6.2.2  vim-textobj-entire
- v + a + e 删除所有文本（前后有空格会删除）
- v + i + e 删除所有有效文本（前后有空格不删除）

# 第七天
## 7.1 滚动屏幕
- 向下滚动一个屏幕 ctrl + f (forward)
- 向上滚动一个屏幕 ctrl + b (backward)
- 向下滚动半个屏幕 ctrl + d
- 向上滚动半个屏幕 ctrl + u
- 向下滚动一行 ctrl + e 
- 向上滚动一行 ctrl + y
- 向上滚动和向下滚动 5 行配置。从以下配置可看出，可以搭配 数字+命令 执行相应的命令
```json
// settings.json
"vim.visualModeKeyBindings": [
        {
            "before":["J"],
            "after":["5","j"]
        },
        {
            "before":["K"],
            "after":["5","k"]
        },

    ],

"vim.normalModeKeyBindings": [
        {
            "before":["J"],
            "after":["5","j"]
        },
        {
            "before":["K"],
            "after":["5","k"]
        },
    ],
```

## 7.2 操作当前行
- zz - 光标行置于屏幕中心 
- zt - 光标行置于屏幕上方
- zb - 光标行置于屏幕下方
## 7.3 跳转到文件首部
gg
## 7.4 跳转到文件尾部
G
## 7.5 跳转到指定行
数字 + gg
数字 + G
# 第八天 
## 8.1 单行搜索
- f - 从左到右搜索符号/单个字母，并且定位到搜索到的内容处，使用分号进入下一个位置，使用逗号返回上一个位置（f + 符号/单个字母）
- F - 从右到左搜索符号/单个字母，并且定位到搜索到的内容处，使用分号进入下一个位置，使用逗号返回上一个位置（F + 符号/单个字母）
- t - 从左到右搜索符号/单个字母，并且定位到搜索到的内容前一个位置，使用分号进入下一个位置，使用逗号返回上一个位置（t + 符号/单个字母）
- T - 从右到左搜索符号/单个字母，并且定位到搜索到的内容后一个位置，使用分号进入下一个位置，使用逗号返回上一个位置（T + 符号/单个字母）

神奇的组合 
- d(操作符，比如 c/v 等都可以) + t(搜索的四个字符) + 字符 删除该行这个字符之前的所有数据

## 8.2 全局查找
- 斜杠(/) 即可进入全局搜索，不区分大小写，输入完成之后回车，再使用 n/N 进行定位
- 问号(?) 即可进入全局搜索，不区分大小写，输入完成之后回车，再使用 n/N 进行定位
- / + 上下左右，即可看到搜索记录
![[Pasted image 20220709165800.png]]
- \# 全局搜索光标所在单词，区分大小写（从下至上）
- \* 全局搜索光标所在单词，区分大小写（从上至下）
# 第九天 更高效的移动
## 9.1 easymotion
```json 
// settings.json
"vim.easymotion": true,
"vim.leader": "<Space>",
```
按照以上配置，改完之后，可以使用以下组合进入 easymotion 模式。
- 操作单词：连续按两次空格+w/e/b/ge (原本是 两次反斜杠+w/e/b/ge)
- 操作行：连续按两次空格+j/k
- 操作单词前后：连续按两次空格 + h/l
- 显示以上三种：连续按三次空格 + j
## 9.2 seak 
```json 
// settings.json
"vim.sneak": true,
```
配置完成之后，按 s 进入 seak 模式
- s/S + 两个字母即可 向下/向上 搜索，分号下一个位置，逗号返回上一个位置

开启 sneak 之后会存在把之前的 s 的功能覆盖掉，且 sneak 的功能和 f 的功能高度重合，所以可以直接使用 sneak 的功能去覆盖掉 f 的功能，配置如下
```json
// settings.json
// normal 模式
"vim.normalModeKeyBindingsNonRecursive": [
        {
            "before":["f"],
            "after":["s"]
        },
        {
            "before":["F"],
            "after":["S"]
        },
        {
            "before":["s"],
            "after":["c","l"]
        },
        {
            "before":["S"],
            "after":["^","C"]
        },
    ],
// 可视化模式
"vim.visualModeKeyBindingsNonRecursive": [
        {
            "before":["f"],
            "after":["s"]
        }
    ],
// 操作模式
"vim.operatorPendingModeKeyBindingsNonRecursive": [
        {
            "before":["f"],
            "after":["z"]
        },
        {
            "before":["F"],
            "after":["Z"]
        },
    ],
```


# 第十天
## 10.1 重复执行操作（数字组合）
- 操作符(d/c/y)/操作符组合 + 数字 
- 数字  + 操作符(d/c/y)/操作符组合 
## 10.2 重复执行操作（点）
- 重复执行上一次操作（例如对文本进行了 新增，修改，删除）,一定要注意是上一次，不包括移动的操作
- 比如执行删除单词操作，如果说当前光标在单词末尾，有三种快捷的方式删除，dbx、bde、diw 。如果我们想要重复上一次的操作删除一个单词，会发现只有 diw 生效，因为 第一个和第二个都包括了移动
- 比如执行在所有行末尾添加分号的操作，可以使用 A + ; 。然后重复按 . 进行操作。(由于这里的 A 包括了移动到末尾并插入，故还是会被记录)
- 替换单词，比如全局搜索某个单词之后，进行 cw 之后，替换成想要的单词，切换到下一个位置，按 . 即可重复上一次操作

# 第十一天 文件移动
## 11.1 、定位
使用场景：比如我发现某个文件我还没有导入，我们可以在使用这个文件的地方打上标记，去写开头写导入逻辑，然后定位回来即可
- 单文件：在某个文件里面 m + 任意一个小写字母，该行会被打上标记，我们可以使用 单引号(\')+之前的任意小写字母 跳转到标记的行，使用 \`+之前的任意小写字母 跳转到标记的行和列
- 多文件和单文件一致，换成大写 M 即可
## 11.2、  查看函数引用
gd。如果出现多个文件调用的情况，使用 l 展开，h 收缩
## 11.3 、跳转
vim 会自动记录一些跳转命令，比如我们使用的 搜索(/、?)、\'、\`、n、N、gg、gd 等命令都会被记录到跳转历史里面，切换文件也会被记录到跳转历史里面，我们可以使用 ctrl+o 或者 ctrl+i 去回到或者下一个历史记录里面
## 11.4 跳转记录 
:jumps

# 第十二天 处理包裹字符串
## 12.1 替换指定的字符
c + s + 要替换掉的字符 + 目标字符
## 12.2 添加指定的字符
y + s + 范围 + 字符
## 12.2 删除指定的字符
d + s + 存在的字符
## 12.3 可视化模式的操作
v/V + S + 以上三个操作都行

# 第十三天 替换
## 13.1 替换命令
需要注意前面就是有个冒号
:\[ranges\]s\[ubstitule\]/{pattern}/{string}/{flags}
参数说明
- range: 范围，可以取的值包括 
	- $到尾部 
	- %全文
	- number,number 从多少行到多少行
- pattern: 需要替换的正则表达式匹配的字符串
- flags:  range 范围内只会匹配每行的第一个单词
	- g 会匹配所有单词
	- c 会有提示问你是否替换
	- gc 可以一起使用
## 13.2 可视化模式下替换
这个用的更多，同是不会有 13.1 中的某些限制
## 13.3 多选操作 
gb 区分大小写，且可以多次按，选中第一次标记的单词

# 第十四天 悬浮显示&大小写&注释
## 14.1 显示悬浮
gh 命令
## 14.2 大小写
### 14.2.1 normol 模式下
- gu + 范围命令 小写
- gU + 范围命令 大写
### 14.2.2 可视化模式下
- u + 范围命令 小写
- U + 范围命令 大写
### 14.2.3 大小写切换
- \~ 波浪号命令
## 14.3 注释
- gc 单行注释
- gC 多行注释

# 第十五天 窗口命令的管理
## 15.1 新建窗口
- ctrl + w + v 左右
- ctrl + w + s 上下
- ctrl + \
## 15.2 关闭窗口
- ctrl + w + c 关闭单个
- ctrl + k + w 关闭所有
## 15.3 窗口切换
### 15.3.1 方法一
使用 shift + 上下左右 方向键
配置 keybindings.json 文件
该文件在 C:\\Users\\USER\\AppData\\Roaming\\Code\\User 下，添加如下配置
```json  
//  keybindings.json
 {
         "key": "shift+left",
        "command": "vim.remap",
        "when": "vim.mode == 'Normal'",
        "args":{
            "after":["<c-w>","h"]
        }
    },
    {
         "key": "shift+right",
        "command": "vim.remap",
        "when": "vim.mode == 'Normal'",
        "args":{
            "after":["<c-w>","l"]
        }
    },
    {
         "key": "shift+up",
        "command": "vim.remap",
        "when": "vim.mode == 'Normal'",
        "args":{
            "after":["<c-w>","k"]
        }
    },
    {
         "key": "shift+down",
        "command": "vim.remap",
        "when": "vim.mode == 'Normal'",
        "args":{
            "after":["<c-w>","j"]
        }
    },
```

### 15.3.2 方法二
ctrl + shift + hjkl
### 15.3.3 方法三和四
ctrl + w + hjkl
ctrl + w + w 

# 第十六天  删除函数
## 16.1 %号的使用
在 光标在 小括号、中括号或者大括号上，可以匹配到相对应的另一个符号上
## 16.2 vim-indent-object
光标需要在函数内部
操作符 + i + i 会删除函数内部所有数据
操作符 + a+ i 会删除函数内部所有数据 + 函数一边
操作符 + a+ I 会删除整个函数
## 16.3 根据方式删除
- dap 基于段落删除，即删除到空行之前
- dal 基于 vim-indent-object 
- 光标在函数 function 所在行，需要根据实际情况，用 V$%d 删除函数

# 第十七天 掌握宏
## 17.1 过程 
开始录制（ q）、结束录制 （q） 、查看录制好的宏( :reg + 空格 +  宏的名称)、使用 （@ 宏的名称）、调用最后一次录制的宏 （@@）、重复执行 （数字+@宏的名称）
安全机制、追加
## 17.2 实际的过程
q完了之后，输入宏的名称，然后录入宏，再来一次q代表录制完成。
比如我需要把以下这段代码 点(.) 替换成 反括号\)，再把首字母大写，
需要录入的按的按键如下 
q + a + 0 + f + . + 空格 + r + ) + w + ~ + j + q 
q：代表开始录制
a：表示宏的名称，后续可以用 @a 去重新执行宏
0：表示到行首
f：搜索
.+空格：光标定位到 . 
r + ) ：替换
w：移动到下一个单词词首
~：切换大小写
j：移动到下一行
q：结束录制
```js
1. one
2. two
10. three
```
按照上述顺序录制完成之后，@a 可以重复调用，也可以使用 5@a 
## 17.3 追加宏
q + 宏的名称（大写的字母）
## 17.4 修改一个已知的宏
取出来 ：
- 双引号 （\"） + 宏名称 +p
- :put + a
修改 :
双引号 （\"） + 宏名称 +yw
双引号 （\"） + 宏名称 +yy
# 第十八天 调用 vscode 命令
## 18.1 格式化文档
- 自带的 alt + shit + f
- 配置之后 leader + f + d
```json
// settings.json
{
	"before":["<Leader>","f","d"],
	"commands":["editor.action.formatDocument"]
},
```

## 18.2 变量重命名
- 自带的 f2
- 配置之后 leader + r + n
```json
// settings.json
{
	 "before":["<Leader>","r","n"],
     "commands":["editor.action.rename"]
},
```

### 18.3 折叠和展开代码
- 自带的 ctrl + \{/\}
- 配置之后 leader + \[/\]
```json
// settings.json
{
	"before":["<Leader>","["],
	"commands":[
		{
			"command": "editor.fold"
		}
	]
},
{
	"before":["<Leader>","]"],
	"commands":[
		{
			"command": "editor.unfold"
		}
	]
},
```


# 第十九天 操作 vscode 
## 19.1 定位到 资源管理器
vscode 自带的 ctrl + shift + e
也可以配置之后使用 ctrl + ;
```json
// keybindings.json
{
  "key": "ctrl+;",
  "command": "workbench.view.explorer",
  "when": "viewContainer.workbench.view.explorer.enabled"
},

```
## 19.2 定位到 编辑区域
- 自带的 ctrl  + 1
- 修改之后用 ctrl + \'
```json
// keybindings.json
{
  "key": "ctrl+;",
  "command": "workbench.view.explorer",
  "when": "viewContainer.workbench.view.explorer.enabled"
},

```
## 19.3 在资源管理器上移动
jk 上下移动
h 定位到 父文件夹上
## 19.4 添加文件
- 在 资源管理器上 添加文件 : a
在 vscode 的 keybord 里面搜索 newFile，之后 复制，然后去 keybindings.json 修改快捷键
```json
// keybindings.json
{
  "key": "a",
  "command": "explorer.newFile",
  "when":"filesExplorerFocus && !inputFocus"
},
```
- 在 编辑区域 添加文件 : leader + n +f
```json
// settings.json
{
	"before":["<Leader>","n","f"],
	"commands":["explorer.newFile"]
},
```
- 使用插件 file utils 
## 19.5 添加文件夹
```json
// keybindings.json
{
  "key": "shift+a",
  "command": "explorer.newFile",
  "when":"filesExplorerFocus && !inputFocus"
},
```

## 19.6 重命名文件夹
keyboard 搜索 rename 
- 自带的 F2
- 配置之后 r
```json
// keybindings.json
{
  "key": "r",
  "command": "renameFile",
  "when": "explorerViewletVisible && filesExplorerFocus && !explorerResourceIsRoot && !explorerResourceReadonly && !inputFocus"
}
```
## 19.6 删除
- 自带的 delete 键
- 快捷键 d
```json
// keybindings.json
{
  "key": "d",
  "command": "deleteFile",
  "when": "explorerViewletVisible && filesExplorerFocus && !explorerResourceReadonly && !inputFocus"
}
```



# 其他无意中发现的快捷键
- 折叠和展开代码 ctrl + \{/\}

# 所有的配置

```json
// settings.json
"vim.easymotion": true,

    "vim.leader": "<Space>",

    "vim.sneak": true,

    // "vim.surround": true,

    "vim.normalModeKeyBindingsNonRecursive": [

        {

            "before":["f"],

            "after":["s"]

        },

        {

            "before":["F"],

            "after":["S"]

        },

        {

            "before":["s"],

            "after":["c","l"]

        },

        {

            "before":["S"],

            "after":["^","C"]

        },

    ],

    "vim.visualModeKeyBindings": [

        {

            "before":["J"],

            "after":["5","j"]

        },

        {

            "before":["K"],

            "after":["5","k"]

        }

    ],

    "vim.visualModeKeyBindingsNonRecursive": [

        {

            "before":["f"],

            "after":["s"]

        }

    ],

    "vim.operatorPendingModeKeyBindingsNonRecursive": [

        {

            "before":["f"],

            "after":["z"]

        },

        {

            "before":["F"],

            "after":["Z"]

        },

    ],

    "vim.handleKeys": {

        "<C-c>": false,

        "<C-f>": true,

        "<C-w>": false,

        "<C-a>": false,

        "<C-v>": true,

    },

    "vim.normalModeKeyBindings": [

        {

            "before":["H"],

            "after":["^"]

        },

        {

            "before":["L"],

            "after":["g","_"]

        },

        {

            "before":["J"],

            "after":["5","j"]

        },

        {

            "before":["K"],

            "after":["5","k"]

        },

    ],

    "vim.operatorPendingModeKeyBindings": [

        {

            "before":["H"],

            "after":["^"]

        },

        {

            "before":["L"],

            "after":["g","_"]

        }

    ],

    "vim.insertModeKeyBindings": [

        {

            "before":["j","j"],

            "after":["<Esc>"]

        }

    ],
```