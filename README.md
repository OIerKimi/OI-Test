# test.sh 自动化编译与测试工具

`test.sh` 是一个用于自动编译和运行 C/C++/Java 程序的自动化工具。它支持单组或多组测试用例，能够自动识别编程语言，并在控制台以彩色输出结果。该工具适用于编程竞赛、自动化测试以及编程学习等场景。

## 目录

- [功能](#功能)
- [前提条件](#前提条件)
- [安装](#安装)
- [使用方法](#使用方法)
  - [运行脚本](#运行脚本)
  - [命令选项](#命令选项)
- [配置说明](#配置说明)
- [测试用例管理](#测试用例管理)
  - [单组测试用例](#单组测试用例)
  - [多组测试用例](#多组测试用例)
- [结果解释](#结果解释)
- [示例](#示例)
- [注意事项](#注意事项)
- [贡献与反馈](#贡献与反馈)
- [许可证](#许可证)

## 功能

- **多语言支持**：支持 C、C++ 和 Java 程序的编译与运行。
- **单组或多组测试用例**：可选择单个测试用例或批量测试多个用例。
- **自动识别编程语言**：根据源代码文件自动识别所使用的编程语言。
- **编译与运行**：自动编译源代码并执行测试用例。
- **结果比较**：自动将程序输出与标准答案进行比较，判断测试结果。
- **彩色输出**：使用 ANSI 颜色代码，美化控制台输出结果。
- **预估分数**：根据测试结果计算预估分数。
- **Docker 支持**：可选使用 Docker 容器隔离运行环境，增强安全性和兼容性。
- **自动清理**：测试完成后自动删除生成的可执行文件和临时文件。

## 前提条件

- **操作系统**：建议在基于 Ubuntu/Debian 的 Linux 系统上运行。
- **必备软件**：
  - `bash`（通常预装在 Linux 系统中）
  - 编程语言对应的编译器：
    - C：`gcc`
    - C++：`g++`
    - Java：`javac`
- **可选软件**：
  - `Docker`：如果选择启用 Docker 支持，脚本会自动检测并安装 Docker（仅适用于 Ubuntu/Debian 系统）。

## 安装

1. **下载脚本**：

   将 `test.sh` 下载到您的项目目录中。

2. **赋予执行权限**：

   ```bash
   chmod +x test.sh
   ```

3. **安装 Docker（可选）**：

   如果您计划使用 Docker 支持，确保您的系统能够安装 Docker。脚本在启用 Docker 支持时会自动安装 Docker（适用于 Ubuntu/Debian 系统）。

## 使用方法

### 运行脚本

在项目目录下运行脚本：

```bash
./test.sh
```

### 命令选项

- `-h`, `--help`：显示帮助信息。

例如，查看帮助信息：

```bash
./test.sh --help
```

## 配置说明

脚本会在当前目录生成一个 `.test_sh_config` 配置文件，用于保存上一次的配置选项。下次运行脚本时，可以选择是否使用上一次的配置，简化操作流程。

## 测试用例管理

### 单组测试用例

适用于仅有一个输入和一个预期输出的测试场景。

**所需文件**：

- **输入文件**：如 `in.txt`
- **答案文件**：如 `ans.txt`

**使用步骤**：

1. 运行脚本并选择“单组样例”。
2. 按提示输入输入文件和答案文件的路径。

### 多组测试用例

适用于有多个测试样例的场景，常见于编程竞赛。

**文件结构**：

测试用例应存放在指定的测试用例目录（默认 `./test_cases`）中。每组测试用例包括一个输入文件和一个对应的答案文件，命名方式如下：

- **输入文件**：`1.in`, `2.in`, `3.in`, ...
- **答案文件**：`1.ans`, `2.ans`, `3.ans`, ... 或 `1.out`, `2.out`, `3.out`, ...

**使用步骤**：

1. 将所有测试用例文件按上述命名规则放入测试用例目录。
2. 运行脚本并选择“多组样例”。
3. 按提示输入测试用例目录的路径（默认为 `./test_cases`）。

## 结果解释

测试完成后，脚本会在控制台输出每个测试用例的结果，并总结总体表现。结果状态包括：

- **AC（Accepted）**：程序输出与标准答案完全一致。
- **WA（Wrong Answer）**：程序输出与标准答案不一致。
- **TLE（Time Limit Exceeded）**：程序运行时间超过设定的时间限制。
- **MLE（Memory Limit Exceeded）**：程序运行过程中使用的内存超过设定的限制。
- **RE（Runtime Error）**：程序在运行过程中发生错误。
- **UKE（Unknown Error）**：无法确定的错误或缺失的答案文件。

此外，脚本会计算并显示预估分数，基于所有测试用例的 AC 数量占总测试用例的比例。

## 示例

### 单组测试示例

假设您的源代码基名称为 `main`，对应文件为 `main.cpp`。测试用例包括 `in.txt` 和 `ans.txt`。

1. 运行脚本：

   ```bash
   ./test.sh
   ```

2. 按照提示选择：

   - 是否启用 Docker：根据需要选择 `Y` 或 `N`。
   - 输入源代码基名称：按默认直接回车（`main`）。
   - 选择样例类型：输入 `1` 选择单组样例。
   - 输入输入文件路径：按默认直接回车（`in.txt`）。
   - 输入答案文件路径：按默认直接回车（`ans.txt`）。
   - 设置时间限制和内存限制：根据需要输入，或按默认值回车。

脚本将自动编译 `main.cpp`，运行程序并比较输出，最后输出测试结果和预估分数。

### 多组测试示例

假设您的源代码基名称为 `main`，对应文件为 `main.java`。测试用例存放在 `./test_cases` 目录下，包括 `1.in`, `1.ans`, `2.in`, `2.ans` 等。

1. 运行脚本：

   ```bash
   ./test.sh
   ```

2. 按照提示选择：

   - 是否启用 Docker：根据需要选择 `Y` 或 `N`。
   - 输入源代码基名称：按默认直接回车（`main`）。
   - 选择样例类型：输入 `2` 选择多组样例。
   - 输入测试用例目录路径：按默认直接回车（`./test_cases`）。
   - 设置时间限制和内存限制：根据需要输入，或按默认值回车。

脚本将自动编译 `main.java`，批量运行所有测试用例，并在控制台输出每个测试的结果及最终的预估分数。

## 注意事项

- **源代码命名**：确保源代码文件名与基名称匹配，并具有正确的文件扩展名（`.c`, `.cpp`, `.java`）。
- **测试用例文件**：在多组测试模式下，确保每个输入文件都有对应的答案文件，且命名规则一致。
- **Docker 权限**：如果选择启用 Docker，确保当前用户有权限运行 Docker 命令，或以具有相应权限的用户运行脚本。
- **资源限制**：合理设置时间和内存限制，以避免测试过程中资源耗尽导致的错误。
- **错误处理**：脚本会在编译失败或其他关键错误时终止运行，并输出相关错误信息。

## 贡献与反馈

欢迎提交 [Issue](https://github.com/OIerKimi/OI-Test/issues) 或 [Pull Request](https://github.com/OIerKimi/OI-Test/pulls) 以改进本工具。您的反馈和贡献将帮助我们不断优化和完善 `test.sh`。

## 许可证

本项目采用 [MIT 许可证](LICENSE)。详情请参阅 LICENSE 文件。

# 致谢

感谢所有为本项目提供支持和建议的开发者和用户。希望 `test.sh` 能为您的编程工作带来便利！

# 联系方式

如有任何问题或建议，请通过 [GitHub Issues](https://github.com/OIerKimi/OI-Test/issues) 与我们联系。

# 免责声明

本工具在设计时尽量考虑了各种使用场景和可能的错误，但不保证在所有环境下均能完美运行。使用者应自行承担使用本工具可能带来的风险。

# 版本历史

- **1.0**：初始发布，支持 C、C++ 和 Java 的编译与测试，提供单组和多组测试用例管理，集成 Docker 支持。

---
