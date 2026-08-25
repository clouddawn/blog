# **LangChain4j**

**LangChain4j** 是一个开源的 Java 库，目标是为 Java 开发者提供一套简单、统一的方式来集成和使用大语言模型（LLM）。

它诞生于2023年初的AI热潮，当时Java生态中缺乏对应的LLM开发工具。虽然名字里有"LangChain"，但它**并非Python版LangChain的简单移植**，而是专门为Java生态从头设计的、符合Java习惯的库。

### 核心理念与特性

LangChain4j 的核心设计理念可以概括为两点：

1. **统一API (Unified APIs)**：各大LLM提供商（如OpenAI）和向量数据库（如Pinecone）都有自己的API。LangChain4j 提供了统一的接口，让你可以在不同服务商之间轻松切换，而无需重写大量代码。
2. **全面的工具箱 (Comprehensive Toolbox)**：它提供了从底层到高层的一系列工具，涵盖了构建LLM应用所需的常见模式和组件。

其主要功能特性包括：

| 功能分类     | 具体特性                                                     |
| :----------- | :----------------------------------------------------------- |
| **模型集成** | 支持 **20+** 个主流LLM提供商（如OpenAI、Google、阿里云等）、**20+** 个嵌入模型和 **5** 个图像生成模型。 |
| **数据存储** | 支持 **30+** 个向量数据库（如Pinecone、Milvus、Chroma等）。  |
| **核心抽象** | 提供提示词模板、聊天记忆管理、工具/函数调用、输出解析器等。  |
| **高级模式** | 支持构建 **RAG（检索增强生成）** 应用、**Agent（智能代理）**。 |
| **框架集成** | 与 **Spring Boot**、**Quarkus**、**Helidon**、**Micronaut** 等主流Java框架无缝集成。 |

### 快速上手：一个简单的例子

以下是使用 LangChain4j 调用 OpenAI 模型的最简步骤。

**第一步：添加依赖**

LangChain4j 的每个集成都是独立的模块。以 Maven 为例，你需要添加核心库和对应 LLM 提供商的依赖：

```xml
<dependency>
    <groupId>dev.langchain4j</groupId>
    <artifactId>langchain4j</artifactId>
    <version>1.11.8</version> <!-- 请使用最新版本 -->
</dependency>
<dependency>
    <groupId>dev.langchain4j</groupId>
    <artifactId>langchain4j-open-ai</artifactId>
    <version>1.11.8</version>
</dependency>
```

> 注意：LangChain4j 要求 **JDK 17 或更高版本**。

**第二步：编写代码**

```java
import dev.langchain4j.model.openai.OpenAiChatModel;
import dev.langchain4j.model.chat.ChatLanguageModel;

public class QuickStart {
    public static void main(String[] args) {
        // 1. 创建模型实例，设置API Key和模型名称
        ChatLanguageModel model = OpenAiChatModel.builder()
                .apiKey(System.getenv("OPENAI_API_KEY")) // 建议从环境变量读取
                .modelName("gpt-4o") // 或 "gpt-3.5-turbo" 等
                .build();

        // 2. 发送消息并获取回复
        String answer = model.chat("你好，请用一句话介绍自己。");
        System.out.println(answer);
    }
}
```

### 与 Spring Boot 的深度集成

对于 Spring Boot 开发者，LangChain4j 提供了专门的 `starter`，可以让你通过 `application.properties` 文件进行配置，极大简化了使用。

1. **添加 Starter 依赖**：

   ```xml
   <dependency>
       <groupId>dev.langchain4j</groupId>
       <artifactId>langchain4j-open-ai-spring-boot-starter</artifactId>
       <version>1.17.0-beta27</version> <!-- 请使用与核心库匹配的版本 -->
   </dependency>
   ```

2. **在 application.properties 中配置**：

   ```properties
   langchain4j.open-ai.chat-model.api-key=${OPENAI_API_KEY}
   langchain4j.open-ai.chat-model.model-name=gpt-4o
   ```

3. **在代码中直接注入使用**：

   ```java
   import dev.langchain4j.model.chat.ChatLanguageModel;
   import org.springframework.web.bind.annotation.GetMapping;
   import org.springframework.web.bind.annotation.RestController;
   
   @RestController
   public class ChatController {
       private final ChatLanguageModel chatModel;
   
       public ChatController(ChatLanguageModel chatModel) {
           this.chatModel = chatModel;
       }
   
       @GetMapping("/chat")
       public String chat(String message) {
           return chatModel.chat(message);
       }
   }
   ```

   这样，一个简单的AI聊天接口就完成了。

### 总结

LangChain4j 可以被看作是Java开发者在LLM时代的“瑞士军刀”。它通过提供统一的API和丰富的工具箱，填补了Java生态在AI应用开发领域的空白，让Java开发者能够以熟悉的方式、较低的学习成本，将大语言模型的能力集成到企业级应用中。

如果想了解更多，可以访问其[官方文档](https://docs.langchain4j.dev/)或查看[官方示例仓库](https://github.com/langchain4j/langchain4j-examples)。