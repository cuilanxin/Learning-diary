## vi/vim 的使用

### 基本上 vi/vim 共分为三种模式，分别是命令模式（Command mode），插入模式（Insert mode）和底线命令模式（Last line mode）

 

### 用户刚刚启动 vi/vim，便进入了命令模式。
- 命令模式 ----> 输入模式：按字母i

- 输入模式 ----> 命令模式：按键ESC

- 命令模式 ----> 底线命令模式：按英文:，再输入命令。


## 各模式下常用命令

### 命令模式

- x  删除当前光标所在处的字符。

## 输入模式

|   ENTER(回车键)    |                          换行                       |
|:------------------:|:-------------------------------------------------------:|
| BACK SPACE(退格键) |                   删除光标前一个字符                   |
|       方向键       |                    在文本中移动光标                    |
|      HOME/END      |                   移动光标到行首/行尾                 |
|         dd         |                 删除游标所在的那一整行                 |
|        ndd         | n 为数字。删除光标所在的向下 n 行(包括游标所在的那一行)    |
|         yy         |                  复制游标所在的那一行                 |
|        nyy         |            n 为数字。复制光标所在的向下 n 行           |
|         p          |            为将已复制的数据在光标下一行贴上             |
|         P          |            为将已复制的数据在光标上一行贴上             |
|         u          |                          撤销                      |

## 底线命令模式

- :w     将编辑的数据写入硬盘档案中
- :w!     强制将编辑的数据写入硬盘档案中
- :q     离开
- :wq     储存后离开
- :wq!   强制储存后离开
- :set nu     　　显示行号，设定之后，会在每一行的前缀显示该行的行号
- :set nonu  　  取消行号

# [iterm语法官网](https://cnbin.github.io/blog/2015/06/20/iterm2-kuai-jie-jian-da-quan/)

1、新建标签：command + t
2、关闭标签：command + w
3、切换标签：command + 数字 command + 左右方向键
4、切换全屏：command + enter
5、查找：command + f

分屏
1、垂直分屏：command + d
2、水平分屏：command + shift + d
3、切换屏幕：command + option + 方向键 command + [ 或 command + ]
4、查看历史命令：command + ;
5、查看剪贴板历史：command + shift + h

自带快捷键
1、⌘ + 数字在各 tab 标签直接来回切换
2、选择即复制 + 鼠标中键粘贴，这个很实用
3、⌘+ f 所查找的内容会被自动复制
4、⌘ + d 横着分屏 / ⌘ + shift + d 竖着分屏
5、⌘ + r = clear换到新一屏，不会想 clear 一样创建一个空屏
6、command + r 清屏
7、输入开头命令后 按 ⌘ + 会自动列出输入过的命令
8、⌘+ shift + h 会列出剪切板历史
可以在 Preferences > keys 设置全局快捷键调出 iterm，这个也可以用过 Alfred 实现


touch  mkdir cp