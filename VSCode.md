# VS Code

--------------------------------------------------------------------------------

# 快捷键 shortcuts

[Mac 下的快捷键列表](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-macos.pdf)，也可以通过 Preferences -> Keyboard Shortcuts 察看或者重设快捷键。

**⌥⌘P** ，调出命令列表，从这里可以看到所有的快捷操作。

## 文本选择

⌃⇧⌘→ - AST (Abstract Syntax Tree) 抽象语法树选择展开一级<br>
⌃⇧⌘← - 抽象语法树选择缩小一级<br>
F2 - 重命名当前对象，或使用鼠标右键菜单<br>
⌘F2 - 重命名当前字符串（包含作为子字符串的情况），或使用鼠标右键菜单<br>
⌃→ - 以单词为单位向后移动光标<br>
⌃⇧→ - 以单词为单位向后选中文本<br>

## 单行编辑

⇧⌘K - 单行操作，删除光标所在行<br>
⇧⌥↓ - 复制光标所在行到下一行<br>
⌥↓ - 将光标所在行移至下一行<br>

## 多行编辑

⌥⌘↓ - 向下插入一个光标，或者使用 ⌥ + Click<br>
⇧⌥ + 鼠标拖动 - 多列区块选择，再配合 ⇧⌘→ 可选中至结尾处<br>
⇧⌘L - 选择相同文本<br>
⌘F2 - 选择相同单词，或者使用 ⌘D 依次加入选中<br>

## 代码定位

⇧⌘\ - 跳转至对应匹配括号处<br>
⇧⌘O - 跳转至对象、属性、方法<br>
⌃G - 跳转至指定行<br>
⌘↓ - 跳转至文件结尾<br>
⇧⌘M - 显示当前文件的错误与警告信息<br>
F12 - 跳转至定义行<br>
⌥F12 - 浮窗打开定义行（可直接修改）<br>
⌥⌘ + Click - 新开侧边窗口跳转至定义行<br>
⇧⌘G - 选中上一次的查找结果<br>

## 代码展示

⌥Z - 开启/关闭代码自动换行，还可通过 editor.wrappingColumn 配置单行最大字符数<br>
⇧⌘[ - 代码折叠，⇧⌥⌘[ 为全部折叠<br>
⇧⌘] - 代码展开，⇧⌥⌘] 为全部展开<br>
⇧⌥F - 代码格式化<br>

## 窗口操作

⌘1 ⌘2 ⌘3 - 切换至对应的子窗口<br>
⌃Tab - 切换当前子窗口的标签页<br>
⌃` - 打开内置 Terminal 窗口<br>
⌘⇧U - 打开/关闭 Output 窗口，可查看 Extensions/Git/Task 输出<br>

--------------------------------------------------------------------------------

# 调试 debug

官网文档 [Debugging](https://code.visualstudio.com/docs/editor/debugging)

## launch / attach

VS Code 调试信息都在配置文件 `.vscode/launch.json` 中 

```json
{
  // Use IntelliSense to learn about possible attributes.
  // Hover to view descriptions of existing attributes.
  // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
  "version": "0.2.0",
  "configurations": [
    {
      "type": "node",
      "request": "launch",
      "name": "Launch",
      "program": "${workspaceFolder}/app.js"
    },
    {
        "type": "node",
        "request": "attach",
        "name": "Attach",
        "port": 5858
    }
  ]
}
```

其中参数 request 的取值有两种 `launch` 和 `attach`

> launch 模式：由 vscode 来启动一个独立 Debug 程序
> attach 模式：附加于一个已经启动的 Debug 程序
