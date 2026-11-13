# Bumi 机器人综合使用手册

将 Bumi 官方综合文档按“认识硬件 → 日常操作 → 准备开发环境 → 调用接口 → 故障排查”重新组织的中文 LaTeX 手册，适合初次使用 Bumi 和准备开展 SDK 开发的读者。

**[阅读 PDF](../bumi-user-manual.pdf)** · [MIT 许可证](LICENSE) · [来源与第三方声明](THIRD_PARTY_NOTICES.md)

本手册是 [Bumi 机器人中文文档](../README.md) 合集之一，源码位于仓库的 `user-manual/` 子目录。

## 内容

| 章节 | 主题 |
| --- | --- |
| 1—2 | 机器人部件与版本、硬件参数、开关机、APP 连接与充电 |
| 3—5 | 终端与虚拟环境、系统架构、网络、SDK 编译与 Docker 环境 |
| 6—7 | HighController、LowController、手柄与 ONNX 策略 |
| 8—9 | MediaController、音频流、视频流与相机采集 |
| 10 | 编译、模块导入、网络、动作和媒体问题排查 |
| 附录 | 控制命令与工作模式、电机错误码、21 个关节参数、资源与视频索引 |

官方资料读取日期为 **2026-11-12**，SDK 接口核对基线为 **3.1.0**。编译与运行 SDK 的 Conda 环境统一为 `bumi_deploy`。这份手册由项目维护者重新编排，官方原文及视频入口见文末资源索引。

## 编译 PDF

安装带有中文支持的 TeX Live，确保 `xelatex` 和 `latexmk` 可用。本项目已在 TeX Live 2025 下编译验证，中文使用 Fandol 字体，代码使用 Latin Modern Mono；流程图使用 TikZ 绘制，部件图保留原有官方图示。

进入本目录（`user-manual/`）后运行：

```sh
latexmk -xelatex -interaction=nonstopmode -halt-on-error main.tex
```

输出为 `_build/main.pdf`。`latexmkrc` 已指定引擎和输出目录，也可以直接执行 `latexmk main.tex`。Conda 用于机器人 SDK 环境，PDF 编译使用 TeX Live。

更新仓库中的阅读版：

```sh
cp _build/main.pdf ../bumi-user-manual.pdf
```

Windows PowerShell 对应命令为：

```powershell
Copy-Item _build/main.pdf ..\bumi-user-manual.pdf
```

### Overleaf

将本目录文件上传到 Overleaf，选择 `main.tex` 为主文件、XeLaTeX 为编译器。正文、图示与样式都包含在仓库内，编译时无需连接官方文档。

## 目录

```text
user-manual/
├── main.tex                   主文件与章节顺序
├── preamble.tex               字体、页眉、提示框、代码与表格
├── frontmatter/               前言
├── chapters/                  10 章正文
├── appendices/                3 个附录
├── images/                    原有官方部件图
├── docs/validation.json       编译校验记录
├── environment.yml            bumi_deploy 环境起点
├── latexmkrc                  编译设置
├── licenses/                  第三方许可证原文
├── THIRD_PARTY_NOTICES.md      来源与第三方材料范围
└── LICENSE                    MIT
```

修改正文时编辑对应章节；修改页眉、字体和提示框时编辑 `preamble.tex`；部件图位于 `images/bumi-components.jpg`。所有 TeX 文件通过本目录内的相对路径引用，工程可独立编译。编译好的阅读版放在仓库根目录的 `../bumi-user-manual.pdf`。

## 开发环境

```sh
conda env create -f environment.yml
conda activate bumi_deploy
```

`environment.yml` 提供 Python 3.10 与 Python 依赖起点。Ubuntu 工具链和 C++ 开发库按正文配置，SDK、训练框架、URDF、镜像和模型通过正文中的上游链接获取。

## 来源与整理范围

- [Bumi 综合使用文档](https://noetixrobotics.feishu.cn/docx/As2adPO27odPBfxQw1ucK6N4nNe)
- [SDK 编译环境部署流程](https://noetixrobotics.feishu.cn/docx/PP2BdXkSUoQ2VOxctJKcEdHanAg)
- [Bumi 音视频开发 MediaController](https://noetixrobotics.feishu.cn/docx/DSXLdLLOXo15vKx4baDcXOfTnue)
- [Bumi SDK](https://github.com/Noetix-Robotics/noetix_sdk_bumi) 与 [Bumi Lab](https://github.com/Noetix-Robotics/noetix_bumi_lab)
- 臧炫懿的 [FAI-for-DBD](https://github.com/ZangXuanyi/fai-for-dbd) 与 [计算机基础能力手册](https://github.com/ZangXuanyi/getting-started-handout)：排版与写作参考。

整理时统一了五参数 `publish_cmd`、C++ `Instance()` 与 Python `instance()` 的写法，以及 `build/example_policy` 目标名称；分别说明运动通信的 2 ms 周期和媒体配置至少 500 ms 的调用间隔。硬件与接口参数整理为表格，原始视频保留在线入口，原有图文内容保持不变。

## 许可与维护

本项目自行编写的内容与排版采用 **MIT**；保留的官方部件图不适用 MIT。SDK 相关示例保留上游 **BSD 3-Clause** 条件，范围与完整声明见 [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md)。实机调试按正文要求使用吊架；PDF 编译记录不作为实机测试记录。

## 修改文档

正文在对应章节文件中修改，公共版式在 `preamble.tex` 中修改。提交修改前重新编译并检查 PDF，把 `_build/main.pdf` 覆盖到仓库根目录的 `../bumi-user-manual.pdf`；编译缓存保留在 `_build/`。
