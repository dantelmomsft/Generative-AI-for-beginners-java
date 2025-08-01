<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "59454ab4ec36d89840df6fcfe7633cbd",
  "translation_date": "2025-07-25T10:50:42+00:00",
  "source_file": "03-CoreGenerativeAITechniques/README.md",
  "language_code": "zh"
}
-->
# 核心生成式 AI 技术教程

## 目录

- [前置条件](../../../03-CoreGenerativeAITechniques)
- [快速开始](../../../03-CoreGenerativeAITechniques)
  - [步骤 1：设置环境变量](../../../03-CoreGenerativeAITechniques)
  - [步骤 2：导航到示例目录](../../../03-CoreGenerativeAITechniques)
- [教程 1：LLM 完成和聊天](../../../03-CoreGenerativeAITechniques)
- [教程 2：函数调用](../../../03-CoreGenerativeAITechniques)
- [教程 3：RAG（检索增强生成）](../../../03-CoreGenerativeAITechniques)
- [教程 4：负责任的 AI](../../../03-CoreGenerativeAITechniques)
- [示例中的通用模式](../../../03-CoreGenerativeAITechniques)
- [下一步](../../../03-CoreGenerativeAITechniques)
- [故障排查](../../../03-CoreGenerativeAITechniques)
  - [常见问题](../../../03-CoreGenerativeAITechniques)

## 概述

本教程通过 Java 和 GitHub Models 提供了核心生成式 AI 技术的实践示例。您将学习如何与大型语言模型（LLM）交互、实现函数调用、使用检索增强生成（RAG）以及应用负责任的 AI 实践。

## 前置条件

在开始之前，请确保您已完成以下准备：
- 安装了 Java 21 或更高版本
- 使用 Maven 进行依赖管理
- 拥有一个 GitHub 账户，并生成了个人访问令牌（PAT）

## 快速开始

### 步骤 1：设置环境变量

首先，您需要将 GitHub 令牌设置为环境变量。此令牌允许您免费访问 GitHub Models。

**Windows（命令提示符）：**
```cmd
set GITHUB_TOKEN=your_github_token_here
```

**Windows（PowerShell）：**
```powershell
$env:GITHUB_TOKEN="your_github_token_here"
```

**Linux/macOS：**
```bash
export GITHUB_TOKEN=your_github_token_here
```

### 步骤 2：导航到示例目录

```bash
cd 03-CoreGenerativeAITechniques/examples/
```

## 教程 1：LLM 完成和聊天

**文件：** `src/main/java/com/example/genai/techniques/completions/LLMCompletionsApp.java`

### 本示例的教学内容

本示例展示了通过 OpenAI API 与大型语言模型（LLM）交互的核心机制，包括使用 GitHub Models 初始化客户端、为系统和用户提示设计消息结构模式、通过累积消息历史管理对话状态，以及通过参数调整控制响应长度和创造力水平。

### 关键代码概念

#### 1. 客户端设置
```java
// Create the AI client
OpenAIClient client = new OpenAIClientBuilder()
    .endpoint("https://models.inference.ai.azure.com")
    .credential(new StaticTokenCredential(pat))
    .buildClient();
```

此代码通过您的令牌连接到 GitHub Models。

#### 2. 简单完成
```java
List<ChatRequestMessage> messages = List.of(
    // System message sets AI behavior
    new ChatRequestSystemMessage("You are a helpful Java expert."),
    // User message contains the actual question
    new ChatRequestUserMessage("Explain Java streams briefly.")
);

ChatCompletionsOptions options = new ChatCompletionsOptions(messages)
    .setModel("gpt-4o-mini")
    .setMaxTokens(200)      // Limit response length
    .setTemperature(0.7);   // Control creativity (0.0-1.0)
```

#### 3. 对话记忆
```java
// Add AI's response to maintain conversation history
messages.add(new ChatRequestAssistantMessage(aiResponse));
messages.add(new ChatRequestUserMessage("Follow-up question"));
```

AI 仅在后续请求中包含之前的消息时，才会记住对话内容。

### 运行示例
```bash
mvn compile exec:java -Dexec.mainClass="com.example.genai.techniques.completions.LLMCompletionsApp"
```

### 运行结果

1. **简单完成**：AI 在系统提示的指导下回答 Java 问题
2. **多轮对话**：AI 在多次提问中保持上下文
3. **交互式聊天**：您可以与 AI 进行真实的对话

## 教程 2：函数调用

**文件：** `src/main/java/com/example/genai/techniques/functions/FunctionsApp.java`

### 本示例的教学内容

函数调用使 AI 模型能够通过结构化协议请求执行外部工具和 API。模型会分析自然语言请求，根据 JSON Schema 定义确定所需的函数调用及其参数，并处理返回结果以生成上下文响应，而函数的实际执行由开发者控制，以确保安全性和可靠性。

### 关键代码概念

#### 1. 函数定义
```java
ChatCompletionsFunctionToolDefinitionFunction weatherFunction = 
    new ChatCompletionsFunctionToolDefinitionFunction("get_weather");
weatherFunction.setDescription("Get current weather information for a city");

// Define parameters using JSON Schema
weatherFunction.setParameters(BinaryData.fromString("""
    {
        "type": "object",
        "properties": {
            "city": {
                "type": "string",
                "description": "The city name"
            }
        },
        "required": ["city"]
    }
    """));
```

此代码告诉 AI 可用的函数及其使用方式。

#### 2. 函数执行流程
```java
// 1. AI requests a function call
if (choice.getFinishReason() == CompletionsFinishReason.TOOL_CALLS) {
    ChatCompletionsFunctionToolCall functionCall = ...;
    
    // 2. You execute the function
    String result = simulateWeatherFunction(functionCall.getFunction().getArguments());
    
    // 3. You give the result back to AI
    messages.add(new ChatRequestToolMessage(result, toolCall.getId()));
    
    // 4. AI provides final response with function result
    ChatCompletions finalResponse = client.getChatCompletions(MODEL, options);
}
```

#### 3. 函数实现
```java
private static String simulateWeatherFunction(String arguments) {
    // Parse arguments and call real weather API
    // For demo, we return mock data
    return """
        {
            "city": "Seattle",
            "temperature": "22",
            "condition": "partly cloudy"
        }
        """;
}
```

### 运行示例
```bash
mvn compile exec:java -Dexec.mainClass="com.example.genai.techniques.functions.FunctionsApp"
```

### 运行结果

1. **天气函数**：AI 请求西雅图的天气数据，您提供数据后，AI 格式化响应
2. **计算器函数**：AI 请求计算（240 的 15%），您计算后，AI 解释结果

## 教程 3：RAG（检索增强生成）

**文件：** `src/main/java/com/example/genai/techniques/rag/SimpleReaderDemo.java`

### 本示例的教学内容

检索增强生成（RAG）通过将外部文档内容注入 AI 提示，将信息检索与语言生成相结合，使模型能够基于特定知识源提供准确答案，而不是依赖可能过时或不准确的训练数据，同时通过策略性提示设计保持用户查询与权威信息源之间的清晰界限。

### 关键代码概念

#### 1. 文档加载
```java
// Load your knowledge source
String doc = Files.readString(Paths.get("document.txt"));
```

#### 2. 上下文注入
```java
List<ChatRequestMessage> messages = List.of(
    new ChatRequestSystemMessage(
        "Use only the CONTEXT to answer. If not in context, say you cannot find it."
    ),
    new ChatRequestUserMessage(
        "CONTEXT:\n\"\"\"\n" + doc + "\n\"\"\"\n\nQUESTION:\n" + question
    )
);
```

三引号帮助 AI 区分上下文和问题。

#### 3. 安全响应处理
```java
if (response != null && response.getChoices() != null && !response.getChoices().isEmpty()) {
    String answer = response.getChoices().get(0).getMessage().getContent();
    System.out.println("Assistant: " + answer);
} else {
    System.err.println("Error: No response received from the API.");
}
```

始终验证 API 响应以防止程序崩溃。

### 运行示例
```bash
mvn compile exec:java -Dexec.mainClass="com.example.genai.techniques.rag.SimpleReaderDemo"
```

### 运行结果

1. 程序加载 `document.txt`（包含有关 GitHub Models 的信息）
2. 您向程序提问有关文档的问题
3. AI 仅基于文档内容回答，而非其一般知识

尝试提问：“什么是 GitHub Models？”与“天气怎么样？”

## 教程 4：负责任的 AI

**文件：** `src/main/java/com/example/genai/techniques/responsibleai/ResponsibleGithubModels.java`

### 本示例的教学内容

负责任的 AI 示例展示了在 AI 应用中实施安全措施的重要性。它演示了检测有害内容类别（包括仇恨言论、骚扰、自残、色情内容和暴力）的安全过滤器，展示了生产环境中的 AI 应用如何通过适当的异常处理、用户反馈机制和备用响应策略优雅地处理内容政策违规。

### 关键代码概念

#### 1. 安全测试框架
```java
private void testPromptSafety(String prompt, String category) {
    try {
        // Attempt to get AI response
        ChatCompletions response = client.getChatCompletions(modelId, options);
        System.out.println("Response generated (content appears safe)");
        
    } catch (HttpResponseException e) {
        if (e.getResponse().getStatusCode() == 400) {
            System.out.println("[BLOCKED BY SAFETY FILTER]");
            System.out.println("This is GOOD - safety system working!");
        }
    }
}
```

#### 2. 测试的安全类别
- 暴力/伤害指令
- 仇恨言论
- 隐私侵犯
- 医疗误导信息
- 非法活动

### 运行示例
```bash
mvn compile exec:java -Dexec.mainClass="com.example.genai.techniques.responsibleai.ResponsibleGithubModels"
```

### 运行结果

程序测试各种有害提示，并展示 AI 安全系统如何：
1. **阻止危险请求**，返回 HTTP 400 错误
2. **允许安全内容**正常生成
3. **保护用户**免受有害 AI 输出的影响

## 示例中的通用模式

### 身份验证模式
所有示例均使用以下模式与 GitHub Models 进行身份验证：

```java
String pat = System.getenv("GITHUB_TOKEN");
TokenCredential credential = new StaticTokenCredential(pat);
OpenAIClient client = new OpenAIClientBuilder()
    .endpoint("https://models.inference.ai.azure.com")
    .credential(credential)
    .buildClient();
```

### 错误处理模式
```java
try {
    // AI operation
} catch (HttpResponseException e) {
    // Handle API errors (rate limits, safety filters)
} catch (Exception e) {
    // Handle general errors (network, parsing)
}
```

### 消息结构模式
```java
List<ChatRequestMessage> messages = List.of(
    new ChatRequestSystemMessage("Set AI behavior"),
    new ChatRequestUserMessage("User's actual request")
);
```

## 下一步

[第 4 章：实践示例](../04-PracticalSamples/README.md)

## 故障排查

### 常见问题

**“GITHUB_TOKEN 未设置”**
- 确保您已设置环境变量
- 验证您的令牌是否具有 `models:read` 权限

**“API 无响应”**
- 检查您的网络连接
- 验证您的令牌是否有效
- 检查是否达到速率限制

**Maven 编译错误**
- 确保您使用的是 Java 21 或更高版本
- 运行 `mvn clean compile` 以刷新依赖项

**免责声明**：  
本文档使用AI翻译服务 [Co-op Translator](https://github.com/Azure/co-op-translator) 进行翻译。尽管我们努力确保翻译的准确性，但请注意，自动翻译可能包含错误或不准确之处。原始语言的文档应被视为权威来源。对于关键信息，建议使用专业人工翻译。我们对因使用此翻译而产生的任何误解或误读不承担责任。