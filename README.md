# Image2LaTEX for Obsidian

**Image2LaTEX** 是一个 Obsidian 插件，它可以将剪贴板中的图像（如数学公式截图）转换为 LaTeX 公式或 Markdown 文本。

本插件集成了多种 OCR 服务商，包括 SimpleTex、Texify、Pix2Tex，以及**自定义 LLM（大语言模型）** 支持。

> 本项目基于 **[obsidian-ocrlatex](https://github.com/Hugo-Persson/obsidian-ocrlatex)** 开发。
> 核心逻辑与架构归功于原作者 **Hugo Persson**。
> 
> This project is a fork/enhanced version based on **[obsidian-ocrlatex](https://github.com/Hugo-Persson/obsidian-ocrlatex)**. All credits for the original idea and core implementation go to **Hugo Persson**. This version extends the functionality to include generic LLM support.

## ✨ 主要功能 (Features)

1.  **剪贴板图像识别**：直接读取剪贴板中的图片进行转换。
2.  **多种转换模式**：
    * **Inline LaTeX**: 行内公式 `$ ... $`
    * **Multiline LaTeX**: 多行公式块 `$$...$$`
    * **Markdown**: 直接转换为 Markdown 文本
3.  **多服务商支持**：
    * **LLM (New!)**: 支持 OpenAI 格式的 API（如 GPT-4o, Claude, 本地模型等），在自定义的prompt下可以适用于Inline/Multiline/包含公式的文本等。
    * **SimpleTex**: 免费且高精度的在线公式识别服务。
    * **Texify**: 自托管的 Markdown 转换服务。
    * **Pix2Tex**: 自托管的 LaTeX OCR 服务。

## 📥 安装 (Installation)

由于这是一个手动构建版本，请按照以下步骤安装：

1.  进入您的 Obsidian 仓库目录：`.obsidian/plugins/`。
2.  新建文件夹 `image2latex`。
3.  将 `main.js`, `manifest.json`, `styles.css` 放入该文件夹。
4.  重启 Obsidian，在“第三方插件”设置中启用 **Image2LaTEX**。

## 🚀 设置与配置 (Configuration)

在 Obsidian 的插件设置页中，您可以选择 LaTeX 和 Markdown 的默认提供商。

### 1. 🤖 LLM (大语言模型) - *推荐*
本版本新增功能。您可以使用任何兼容 OpenAI 接口的模型（如 GPT-4 Vision, Claude 3.5 Sonnet 或本地多模态模型）进行识别。

* **Endpoint**: API 终端地址 (例如: `https://api.openai.com/v1/chat/completions` 或本地 `http://localhost:11434/v1/...`)。
* **Model**: 模型名称 (例如: `gpt-4o`, `gpt-4-turbo`, `llava`)。
* **API Key**: 您的 API 密钥。
* **Max Tokens**: 生成的最大 Token 数 (默认为 300)。
* **Prompts**: 您可以自定义提示词来优化 LaTeX 或 Markdown 的输出结果。

### 2. ☁️ SimpleTex
一个免费且高精度的在线服务（推荐用于 LaTeX）。

1.  访问 [SimpleTex API Dashboard](https://simpletex.cn/api)。
2.  注册/登录账户。
3.  创建一个 Token。
4.  将 Token 粘贴到插件设置的 `SimpleTex Token` 栏中。

### 3. 🏠 Texify (自托管)
适用于将图像转换为 Markdown 文本。

* 需要自托管模型，详见：[texify-web-api](https://github.com/Hugo-Persson/texify-wep-api)。
* 部署后，在设置中填入 API URL (例如 `http://localhost:5000/predict`)。

### 4. 🐳 Pix2Tex (自托管)
LaTeX OCR 的替代方案。

* 可以通过 Docker 或 Python 运行。
* Docker部署: 参考 [pix2tex Docker](https://hub.docker.com/r/lukasblecher/pix2tex)。
* Python部署:
    ```bash
    pip install pix2tex[api]
    python -m pix2tex.api.run
    ```
* 在设置中填入 URL (例如 `http://localhost:8502/predict/`)。

## 🎮 使用方法 (Usage)

1.  截图或复制包含数学公式的图片到剪贴板。
2.  在 Obsidian 中打开命令面板 (`Ctrl/Cmd + P`)。
3.  运行以下命令之一：
    * `Image2LaTEX: Generate inline LaTeX from last image...` (生成行内公式)
    * `Image2LaTEX: Generate multiline LaTeX from last image...` (生成多行公式块)
    * `Image2LaTEX: Generate markdown from last image...` (生成 Markdown)
4.  插件会显示 "Loading latex..."，识别完成后会自动替换为结果。
