### DeepSeek 快速开始教程 🐋
#### 概述
 - 这个仓库包含一个强大的编码助手应用，集成 DeepSeek API，能够处理用户对话并生成结构化的 JSON 响应。用户可以通过命令行界面读取本地文件内容、创建新文件，并实时修改现有文件。

#### 主要功能

1. **DeepSeek 客户端配置**
   - 自动配置 API 客户端，使用有效的 DEEPSEEK_API_KEY 连接 DeepSeek 服务。
   - 根据环境变量指定的 DeepSeek 端点，流式获取 GPT 风格的回复。

2. **数据模型**
   - 使用 Pydantic 进行类型安全的文件操作，主要包括：
     - **FileToCreate**：描述要创建或更新的文件。
     - **FileToEdit**：描述要在现有文件中替换的代码片段。
     - **AssistantResponse**：结构化的聊天回复和可能的文件操作。

3. **系统提示**
   - 一个全面的系统提示（system_PROMPT）引导对话，确保所有回复严格符合 JSON 输出格式，并可包括文件的创建或编辑。

4. **辅助功能**
   - **read_local_file**：读取指定文件路径的内容并返回字符串。
   - **create_file**：创建或覆盖文件，内容由用户提供。
   - **show_diff_table**：以表格形式展示文件修改建议。
   - **apply_diff_edit**：对现有文件应用片段级别的修改。

5. **"/add" 命令**
   - 使用 `/add path/to/file` 快速读取文件内容并将其插入对话中。
   - 使用 `/add path/to/folder` 将目录中的所有文件（排除二进制文件和隐藏文件）添加到对话中。

6. **对话流程**
   - 维护 `conversation_history` 列表，记录用户与助手的消息。
   - 通过 DeepSeek API 流式传输助手的回复，解析为 JSON 格式，确保文本回复和文件修改指令的完整性。

7. **交互式会话**
   - 运行脚本（如 `python3 main.py`）启动交互循环。
   - 输入请求或代码问题，使用 `/add path/to/file` 将文件内容添加到对话中。
   - 当助手提出新或编辑后的文件时，可直接确认更改。
   - 输入 "exit" 或 "quit" 退出会话。

#### 快速入门
0. 如果自己还没有DEEPSEEK_KEY，可以在https://api-docs.deepseek.com/ 花5分钟注册并申请一个，通常官方会提供10元到新账号里。

1. 配置 .env 文件，并添加 DeepSeek API 密钥：
   ```plaintext
   DEEPSEEK_KEY=你的_api_key
   ```

2. 安装依赖并运行（选择其中一种方式）：

   - **使用 pip 安装**：
     ```bash
     git clone --depth 1 https://github.com/XiaomingX/deepseek-quickstart
     pip install -r requirements.txt
     python3 main.py
     ```

3. 体验多行流式响应、使用 "/add path/to/file" 读取文件内容，并在批准后精确编辑文件。

#### 推理版（main-r1.py）

新增 `main-r1.py` 脚本，采用 DeepSeek 推理模型（`deepseek-reasoner`），支持“思维链”（CoT）推理：

- 展示推理过程，然后给出最终答案。
- 保留所有文件操作和差异编辑功能。
- 显示推理过程，并仅记录最终结论。

使用 `python3 main-r1.py`启动，享受推理过程增强体验。

> **注意**：这是 xiaomingx 开发的实验项目，旨在测试 DeepSeek v3 API 的新功能，作为快速原型使用时请注意。

# 更多官方材料
 - 我也在探索中，官方仓库地址是：https://github.com/deepseek-ai