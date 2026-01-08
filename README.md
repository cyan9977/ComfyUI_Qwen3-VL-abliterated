# ComfyUI_Qwen3-VL-abliterated

这是 [Qwen3-VL-Instruct](https://github.com/QwenLM/Qwen3-VL) 在 [ComfyUI](https://github.com/comfyanonymous/ComfyUI) 平台上的实现版本，支持（但不限于）基于文本的查询、视频查询、单图像查询和多图像查询，用于生成标题或回答。

本仓库是基于 [ComfyUI_Qwen3-VL-Instruct](https://github.com/IuvenisSapiens/ComfyUI_Qwen3-VL-Instruct) 的 Fork 版本，**主要增加了对 abliterated（去审查）版本模型的支持**，包括 `huihui-ai/Huihui-Qwen3-VL-4B-Instruct-abliterated` 等模型。

---

## 基本工作流

- **基于文本的查询**：用户可以提交文本查询以请求信息或生成描述。例如，用户可以输入类似"生命的意义是什么？"的描述。

![Chat_with_text_workflow preview](examples/Chat_with_text_workflow.png)

- **视频查询**：当用户上传视频时，系统可以分析内容并为每一帧生成详细标题或整个视频的摘要。例如，"为给定的视频生成标题。"

![Chat_with_video_workflow preview](examples/Chat_with_video_workflow.png)

- **单图像查询**：此工作流支持为单个图像生成标题。用户可以上传照片并询问"这张图片显示了什么？"，结果可能是"一只雄伟的狮子群在草原上休息。"

![Chat_with_single_image_workflow preview](examples/Chat_with_single_image_workflow.png)

- **多图像查询**：对于多张图像，系统可以提供集体描述或将图像联系在一起的叙述。例如，"从以下系列图像中创建一个故事：一对夫妇在海滩上的一张，另一张在婚礼仪式上，最后一张在婴儿的洗礼上。"

![Chat_with_multiple_images_workflow preview](examples/Chat_with_multiple_images_workflow.png)

> [!IMPORTANT]
> 使用工作流的重要提示
> - 请确保您的 ComfyUI 设置中可以使用"Display Text node"。如果遇到此节点缺失的问题，您可以在 [ComfyUI_MiniCPM-V-4_5 仓库](https://github.com/IuvenisSapiens/ComfyUI_MiniCPM-V-4_5) 中找到它。安装此附加组件将使"Display Text node"可供使用。

## 支持的模型

本插件支持以下模型：

### 官方模型
- `Qwen3-VL-4B-Instruct-FP8`
- `Qwen3-VL-4B-Thinking-FP8`
- `Qwen3-VL-8B-Instruct-FP8`
- `Qwen3-VL-8B-Thinking-FP8`
- `Qwen3-VL-4B-Instruct`
- `Qwen3-VL-4B-Thinking`
- `Qwen3-VL-8B-Instruct`
- `Qwen3-VL-8B-Thinking`

### Abliterated 模型（去审查版本）
- `Qwen3-VL-4B-Instruct-abliterated` - 基于 [huihui-ai/Huihui-Qwen3-VL-4B-Instruct-abliterated](https://huggingface.co/huihui-ai/Huihui-Qwen3-VL-4B-Instruct-abliterated)

> **⚠️ 关于 Abliterated 模型的警告**
> 
> - **敏感或争议内容风险**：此模型的安全过滤已显著降低，可能生成敏感、争议或不适当的内容。用户应谨慎使用并严格审查生成的输出。
> - **不适合所有受众**：由于内容过滤有限，模型的输出可能不适合公共环境、未成年用户或需要高安全性的应用。
> - **法律和道德责任**：用户必须确保其使用符合当地法律和道德标准。生成的内容可能带来法律或道德风险，用户需对任何后果负责。
> - **研究和实验用途**：建议将此模型用于研究、测试或受控环境，避免在生产或面向公众的商业应用中直接使用。
> - **监控和审查建议**：强烈建议用户实时监控模型输出，并在必要时进行人工审查，以防止传播不当内容。

## 安装

### 使用 Git Clone 安装

1. 打开终端（Windows 使用 PowerShell 或 CMD，Linux/Mac 使用 Terminal）

2. 进入 ComfyUI 的 `custom_nodes` 目录：
   ```bash
   cd ComfyUI\custom_nodes
   ```

3. 克隆本仓库：
   ```bash
   git clone https://github.com/cyan9977/ComfyUI_Qwen3-VL-abliterated.git
   ```

4. 进入插件目录：
   ```bash
   cd ComfyUI_Qwen3-VL-abliterated
   ```

5. 安装依赖：
   ```bash
   pip install -r requirements.txt
   ```

6. 重启 ComfyUI，插件即可使用。

## 下载模型

所有模型将在运行工作流时自动下载（如果它们在 `ComfyUI\models\prompt_generator\` 目录中未找到）。

### 手动下载模型

如果您想手动下载模型，可以将模型文件夹放置在以下位置：

- **官方模型**：`ComfyUI\models\prompt_generator\Qwen3-VL-4B-Instruct\` 等
- **Abliterated 模型**：`ComfyUI\models\prompt_generator\Qwen3-VL-4B-Instruct-abliterated\`

模型将从 Hugging Face 自动下载：
- 官方模型：`qwen/Qwen3-VL-*`
- Abliterated 模型：`huihui-ai/Huihui-Qwen3-VL-4B-Instruct-abliterated`

## 使用方法

1. 在 ComfyUI 中添加 `Qwen3_VQA` 节点
2. 在模型下拉菜单中选择您想要使用的模型
3. 输入您的文本查询
4. （可选）上传图像或视频
5. 运行工作流

## 关于

本仓库成功将 Qwen3-VL-Instruct 系列集成到 ComfyUI 平台，实现了流畅运行，支持（但不限于）基于文本的查询、视频查询、单图像查询和多图像查询，用于生成标题或回答。

### 资源

- [Qwen3-VL 官方仓库](https://github.com/QwenLM/Qwen3-VL)
- [ComfyUI 官方仓库](https://github.com/comfyanonymous/ComfyUI)
- [原版 ComfyUI_Qwen3-VL-Instruct](https://github.com/IuvenisSapiens/ComfyUI_Qwen3-VL-Instruct)
- [Abliterated 模型页面](https://huggingface.co/huihui-ai/Huihui-Qwen3-VL-4B-Instruct-abliterated)

### 许可证

Apache-2.0 许可证
