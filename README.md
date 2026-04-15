# Mini-C-Compiler

一个用于学习编译原理的 Mini C 编译器示例，使用 C++ 实现了从词法分析到中间代码优化的核心流程。

## 项目目标

- 演示一个教学型编译器的完整前端流程
- 便于理解 LR 语法分析与语义动作
- 通过四元式与 DAG 优化展示中间表示处理

## 已实现能力

- **词法分析**：对源程序进行扫描并生成 Token 序列与符号表  
- **语法分析**：基于 Action/Goto 表进行 LR 分析  
- **语义分析**：进行变量声明、类型与作用域等基础检查  
- **中间代码生成**：生成四元式中间表示  
- **中间代码优化**：按基本块进行 DAG 优化  

## 支持语法（概要）

可在 `grammar.txt` 查看完整文法，当前覆盖：

- 变量声明与函数声明/定义（`int/float/double/void`）
- 表达式：`+ - * /` 与比较运算（`> < >= <= == !=`）
- 语句：赋值、`if/else`、`while`、`return`
- 函数调用与参数列表

## 项目结构

```text
Mini-C-Compiler
├─ ActionAndGoto.txt         # LR 分析表
├─ grammar.txt               # 文法定义
├─ tablist.txt               # 项目集相关数据
├─ text.txt                  # 示例输入程序
├─ textgra.txt               # 文法测试输入
└─ src
   ├─ main.cpp
   ├─ GrammerAnalyzer        # 文法分析与表生成
   │  ├─ analys_gramer.cpp
   │  └─ selectAndtable.h
   ├─ LexicalAnalyzer        # 词法分析
   │  ├─ lexical.cpp
   │  └─ lexical.h
   ├─ Parser                 # LR 语法分析 + 语义分析
   │  ├─ analys_LR.cpp
   │  └─ analys_LR.h
   ├─ IntermediateCode       # 四元式与基本块
   │  ├─ common.cpp
   │  ├─ common.h
   │  ├─ IntermediateCode.cpp
   │  └─ IntermediateCode.h
   └─ Optimize               # DAG 优化
      ├─ optimize.cpp
      └─ optimize.h
```

## 快速开始

### 1) 克隆仓库

```bash
git clone https://github.com/ChuanruiWu/Mini-C-Compiler.git
cd Mini-C-Compiler
```

### 2) 编译（示例）

> 该项目主要按教学/实验环境编写，不同编译器可能存在兼容差异（如 `sprintf_s` 等）。  
> 建议优先使用 Visual Studio（MSVC）环境构建。

在支持环境下，可参考如下命令手动编译：

```bash
g++ -std=c++17 \
  src/main.cpp \
  src/Parser/analys_LR.cpp \
  src/LexicalAnalyzer/lexical.cpp \
  src/IntermediateCode/common.cpp \
  src/IntermediateCode/IntermediateCode.cpp \
  src/Optimize/optimize.cpp \
  src/GrammerAnalyzer/analys_gramer.cpp \
  -Isrc/Parser -Isrc/LexicalAnalyzer -Isrc/GrammerAnalyzer -Isrc/IntermediateCode -Isrc/Optimize \
  -o mini_c_compiler
```

### 3) 运行

程序默认读取仓库根目录下的 `text.txt`：

```bash
./mini_c_compiler
```

运行后会输出：

- Token 序列与符号表
- 语义分析相关信息
- 原始四元式、基本块划分结果与优化后结果

## 使用说明

- 如需替换测试程序，直接修改 `text.txt`。  
- 如需调整语法规则，修改 `grammar.txt`，并通过 `GrammerAnalyzer` 重新生成分析表。  
- `main.cpp` 中已串联词法、语法、语义、中间代码和优化流程，可作为调用示例。  

## 备注

本项目偏向教学用途，当前重点是编译流程演示，工程化能力（跨平台构建、自动化测试等）仍可继续完善。欢迎提交 Issue 或 PR 共同改进。
