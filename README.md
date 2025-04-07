# Gbox 引擎文档

这个仓库包含Gbox 2D游戏引擎的文档、语法参考和示例代码，同时提供了Cursor编辑器的AI辅助配置。

## 项目内容

- **doc/** - 文档目录
  - `gbox_syntax.md` - Gbox脚本语言语法参考
  - `gbox_api.md` - Gbox引擎API文档

- **examples/** - 示例代码目录
  - `simple_game.gb` - 简单游戏示例
  - `enum_example.gb` - 枚举使用示例
  - `preprocessor_example.gb` - 预处理器示例

- **.cursor/** - Cursor编辑器AI配置
  - `rules/gbox.md` - Gbox语法和API规则文件

## 在Cursor中使用Gbox

这个仓库包含了让Cursor编辑器理解Gbox脚本的规则配置。当你在Cursor中编辑`.gb`或`.gbz`文件时，AI会根据这些规则提供更准确的代码建议。

### 快速设置

如何让Cursor的AI助手理解Gbox脚本：

1. **克隆本仓库**
   ```bash
   git clone https://github.com/jinruozai/gbox_docs.git
   # 或
   git clone https://gitee.com/lazygoo/gbox_docs.git
   ```

2. **在仓库中开发**
   你可以直接在克隆的仓库中编写Gbox代码

   或者

3. **复制必要文件到现有项目**
   - 创建必要的目录结构
     ```bash
     mkdir -p path/to/your/project/.cursor/rules
     mkdir -p path/to/your/project/doc
     ```
   
   - 复制规则文件
     ```bash
     cp gbox_docs/.cursor/rules/gbox.md path/to/your/project/.cursor/rules/
     cp gbox_docs/doc/gbox_syntax.md path/to/your/project/doc/
     cp gbox_docs/doc/gbox_api.md path/to/your/project/doc/
     ```

### 文件依赖关系

规则文件`.cursor/rules/gbox.md`通过`@doc/gbox_syntax.md`和`@doc/gbox_api.md`引用文档文件，保持目录结构不变。

## 语法文档

`doc/gbox_syntax.md`包含了完整的Gbox脚本语言语法参考，包括：
- 基础语法（注释、变量）
- 类和对象
- 函数
- 条件和循环
- 样式系统
- 异常处理

## API文档

`doc/gbox_api.md`包含了Gbox引擎的API文档，帮助你了解可用的类、方法和属性。

## 示例

`examples/`目录包含了一些Gbox脚本示例，展示了语言特性和常见用法。 