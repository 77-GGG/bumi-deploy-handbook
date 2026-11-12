# Bumi 机器人笔记本外挂部署手册

面向使用 Ubuntu 笔记本部署 Bumi 运动策略的中文手册。以 `examples/py/test_policy.py` 为主线，先介绍终端、Python、Conda 与网络，再完成 SDK 编译、网线连接、手柄配置、程序启动和退出。

**[阅读 PDF](docs/bumi-deploy-handbook.pdf)** · [MIT 许可证](LICENSE) · [来源与第三方声明](THIRD_PARTY_NOTICES.md)

## 内容

| 部分 | 章节 |
| --- | --- |
| 前置知识 | 终端与 Linux、Python 与 C++、Conda 与虚拟环境、网络通信与机器人控制 |
| 部署实践 | 外挂开发与系统组成、软件环境、网络与手柄、开机与程序启动、操作与退出 |
| 附录 | 手柄按键与控制模式、使用注意事项、常见故障速查 |

编译与运行机器人 SDK 的 Conda 环境统一为 `bumi_deploy`。教程场景为 Ubuntu 22.04 x86_64 笔记本、有线连接 Bumi 运控板、澳加狮手柄和 ONNX 策略推理；软件接口核对基线为 Bumi SDK 3.1.0。实机调试按正文要求使用吊架，并完成停控与稳定支撑后再退出程序。

## 编译 PDF

安装带有中文支持的 TeX Live，确保 `xelatex` 和 `latexmk` 可用。本项目已在 TeX Live 2025 下编译验证，使用 TeX Live 自带的 Fandol 中文字体和 Latin Modern Mono 字体。

在本仓库根目录运行：

```sh
latexmk -xelatex -interaction=nonstopmode -halt-on-error main.tex
```

输出文件为 `_build/main.pdf`。`latexmkrc` 已配置 XeLaTeX 与输出目录，也可以直接运行 `latexmk main.tex`。Conda 用于手册中的 SDK 部署，编译这本手册使用 TeX Live。

更新仓库中的阅读版：

```sh
cp _build/main.pdf docs/bumi-deploy-handbook.pdf
```

Windows PowerShell 对应命令为：

```powershell
Copy-Item _build/main.pdf docs/bumi-deploy-handbook.pdf
```

### Overleaf

上传本仓库文件，选择 `main.tex` 为主文件，将编译器设为 XeLaTeX，再点击编译。章节和公共样式均已包含在本工程内。

## 目录

```text
bumi-deploy-handbook/
├── main.tex                   主文件与章节顺序
├── preamble.tex               字体、页眉、提示框、代码与表格
├── frontmatter/               前言
├── chapters/                  9 章正文
├── appendices/                3 个附录
├── docs/                      可直接阅读的 PDF
├── latexmkrc                  编译设置
├── licenses/                  第三方许可证原文
├── THIRD_PARTY_NOTICES.md      来源与第三方材料范围
└── LICENSE                    MIT
```

修改正文时编辑对应章节，调整字体和页眉时编辑 `preamble.tex`。所有 TeX 引用均为仓库内相对路径，单独下载此目录即可编译。

## 参考与许可

- [Bumi SDK](https://github.com/Noetix-Robotics/noetix_sdk_bumi)
- [Bumi 官方综合手册](https://noetixrobotics.feishu.cn/docx/As2adPO27odPBfxQw1ucK6N4nNe)
- 臧炫懿的 [FAI-for-DBD](https://github.com/ZangXuanyi/fai-for-dbd) 与 [计算机基础能力手册](https://github.com/ZangXuanyi/getting-started-handout)：排版与写作参考。

本项目自行编写的内容与排版采用 **MIT**。SDK 相关示例保留上游 **BSD 3-Clause** 条件，具体范围见 [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md)。

## 修改文档

正文在对应章节文件中修改，公共版式在 `preamble.tex` 中修改。提交修改前重新编译并检查 PDF，更新 `docs/` 中的阅读版；编译缓存保留在 `_build/`。
