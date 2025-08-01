<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "0cbf68d605615a1e602c832a24616859",
  "translation_date": "2025-07-25T10:53:52+00:00",
  "source_file": "04-PracticalSamples/petstory/README.md",
  "language_code": "mo"
}
-->
# 寵物故事生成器初學者教程

## 目錄

- [先決條件](../../../../04-PracticalSamples/petstory)
- [了解專案結構](../../../../04-PracticalSamples/petstory)
- [核心元件解析](../../../../04-PracticalSamples/petstory)
  - [1. 主應用程式](../../../../04-PracticalSamples/petstory)
  - [2. 網頁控制器](../../../../04-PracticalSamples/petstory)
  - [3. 故事服務](../../../../04-PracticalSamples/petstory)
  - [4. 網頁模板](../../../../04-PracticalSamples/petstory)
  - [5. 配置](../../../../04-PracticalSamples/petstory)
- [運行應用程式](../../../../04-PracticalSamples/petstory)
- [整體運作方式](../../../../04-PracticalSamples/petstory)
- [了解 AI 整合](../../../../04-PracticalSamples/petstory)
- [下一步](../../../../04-PracticalSamples/petstory)

## 先決條件

在開始之前，請確保您已經具備以下條件：
- 安裝了 Java 21 或更高版本
- 使用 Maven 進行依賴管理
- 擁有一個 GitHub 帳戶，並設置了具有 `models:read` 權限的個人訪問令牌 (PAT)
- 基本了解 Java、Spring Boot 和網頁開發

## 了解專案結構

寵物故事專案包含以下重要檔案：

```
petstory/
├── src/main/java/com/example/petstory/
│   ├── PetStoryApplication.java       # Main Spring Boot application
│   ├── PetController.java             # Web request handler
│   ├── StoryService.java              # AI story generation service
│   └── SecurityConfig.java            # Security configuration
├── src/main/resources/
│   ├── application.properties         # App configuration
│   └── templates/
│       ├── index.html                 # Upload form page
│       └── result.html               # Story display page
└── pom.xml                           # Maven dependencies
```

## 核心元件解析

### 1. 主應用程式

**檔案:** `PetStoryApplication.java`

這是我們 Spring Boot 應用程式的入口點：

```java
@SpringBootApplication
public class PetStoryApplication {
    public static void main(String[] args) {
        SpringApplication.run(PetStoryApplication.class, args);
    }
}
```

**功能說明:**
- `@SpringBootApplication` 註解啟用自動配置和元件掃描
- 在埠 8080 上啟動嵌入式網頁伺服器 (Tomcat)
- 自動建立所有必要的 Spring beans 和服務

### 2. 網頁控制器

**檔案:** `PetController.java`

負責處理所有網頁請求和使用者互動：

```java
@Controller
public class PetController {
    
    private final StoryService storyService;
    
    public PetController(StoryService storyService) {
        this.storyService = storyService;
    }
    
    @GetMapping("/")
    public String index() {
        return "index";  // Returns index.html template
    }
    
    @PostMapping("/generate-story")
    public String generateStory(@RequestParam("description") String description, 
                               Model model, 
                               RedirectAttributes redirectAttributes) {
        
        // Input validation
        if (description.trim().isEmpty()) {
            redirectAttributes.addFlashAttribute("error", "Please provide a description.");
            return "redirect:/";
        }
        
        // Sanitize input for security
        String sanitizedDescription = sanitizeInput(description);
        
        // Generate story with error handling
        try {
            String story = storyService.generateStory(sanitizedDescription);
            model.addAttribute("caption", sanitizedDescription);
            model.addAttribute("story", story);
            return "result";  // Returns result.html template
            
        } catch (Exception e) {
            // Use fallback story if AI fails
            String fallbackStory = generateFallbackStory(sanitizedDescription);
            model.addAttribute("story", fallbackStory);
            return "result";
        }
    }
    
    private String sanitizeInput(String input) {
        return input.replaceAll("[<>\"'&]", "")  // Remove dangerous characters
                   .trim()
                   .substring(0, Math.min(input.length(), 500));  // Limit length
    }
}
```

**主要功能:**

1. **路由處理**: `@GetMapping("/")` 顯示上傳表單，`@PostMapping("/generate-story")` 處理提交
2. **輸入驗證**: 檢查描述是否為空以及長度限制
3. **安全性**: 清理使用者輸入以防止 XSS 攻擊
4. **錯誤處理**: 當 AI 服務失敗時提供備用故事
5. **模型綁定**: 使用 Spring 的 `Model` 將資料傳遞到 HTML 模板

**備用系統:**
控制器包含預先撰寫的故事模板，當 AI 服務不可用時使用：

```java
private String generateFallbackStory(String description) {
    String[] storyTemplates = {
        "Meet the most wonderful pet in the world – a furry ball of energy...",
        "Once upon a time, there lived a remarkable pet whose heart was as big...",
        "In a cozy home filled with love, there lived an extraordinary pet..."
    };
    
    // Use description hash for consistent responses
    int index = Math.abs(description.hashCode() % storyTemplates.length);
    return storyTemplates[index];
}
```

### 3. 故事服務

**檔案:** `StoryService.java`

此服務負責與 GitHub Models 通訊以生成故事：

```java
@Service
public class StoryService {
    
    private final OpenAIClient openAIClient;
    private final String modelName;
    
    public StoryService(@Value("${github.models.endpoint}") String endpoint,
                       @Value("${github.models.model}") String modelName) {
        
        String githubToken = System.getenv("GITHUB_TOKEN");
        if (githubToken == null || githubToken.isBlank()) {
            throw new IllegalStateException("GITHUB_TOKEN environment variable must be set");
        }
        
        // Create OpenAI client configured for GitHub Models
        this.openAIClient = OpenAIOkHttpClient.builder()
                .baseUrl(endpoint)
                .apiKey(githubToken)
                .build();
    }
    
    public String generateStory(String description) {
        String systemPrompt = "You are a creative storyteller who writes fun, " +
                             "family-friendly short stories about pets. " +
                             "Keep stories under 500 words and appropriate for all ages.";
        
        String userPrompt = "Write a fun short story about a pet described as: " + description;
        
        // Configure the AI request
        ChatCompletionCreateParams params = ChatCompletionCreateParams.builder()
                .model(modelName)
                .addSystemMessage(systemPrompt)
                .addUserMessage(userPrompt)
                .maxCompletionTokens(500)  // Limit response length
                .temperature(0.8)          // Control creativity (0.0-1.0)
                .build();
        
        // Send request and get response
        ChatCompletion response = openAIClient.chat().completions().create(params);
        
        return response.choices().get(0).message().content().orElse("");
    }
}
```

**主要元件:**

1. **OpenAI 客戶端**: 使用配置為 GitHub Models 的官方 OpenAI Java SDK
2. **系統提示**: 設定 AI 的行為以撰寫適合家庭的寵物故事
3. **使用者提示**: 根據描述指示 AI 撰寫具體故事
4. **參數**: 控制故事長度和創意程度
5. **錯誤處理**: 拋出例外，供控制器捕捉並處理

### 4. 網頁模板

**檔案:** `index.html` (上傳表單)

使用者描述寵物的主要頁面：

```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>Pet Story Generator</title>
    <!-- CSS styling -->
</head>
<body>
    <div class="container">
        <h1>Pet Story Generator</h1>
        <p>Describe your pet and we'll create a fun story about them!</p>
        
        <!-- Error message display -->
        <div th:if="${error}" class="error" th:text="${error}"></div>
        
        <!-- Story generation form -->
        <form action="/generate-story" method="post">
            <div class="form-group">
                <label for="description">Describe your pet:</label>
                <textarea id="description" name="description" 
                         placeholder="Tell us about your pet - what they look like, their personality, favorite activities..."
                         maxlength="1000" required></textarea>
            </div>
            <button type="submit" class="btn btn-primary">Generate Story</button>
        </form>
        
        <!-- Image upload section with client-side processing -->
        <div class="upload-section">
            <h2>Or Upload a Photo</h2>
            <input type="file" id="imageInput" accept="image/*" />
            <button onclick="analyzeImage()" class="upload-btn">Analyze Image</button>
        </div>
        
        <script>
            // Client-side image analysis using Transformers.js
            async function analyzeImage() {
                // Image processing code here
                // Generates description automatically from uploaded image
            }
        </script>
    </div>
</body>
</html>
```

**檔案:** `result.html` (故事展示)

顯示生成的故事：

```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>Pet Story Result</title>
</head>
<body>
    <div class="container">
        <h1>Your Pet's Story</h1>
        
        <div class="result-section">
            <div class="result-label">Pet Description:</div>
            <div class="result-content" th:text="${caption}"></div>
        </div>
        
        <div class="result-section">
            <div class="result-label">Generated Story:</div>
            <div class="result-content" th:text="${story}"></div>
        </div>
        
        <div class="result-section" th:if="${analysisType}">
            <div class="result-label">Analysis Type:</div>
            <div class="result-content" th:text="${analysisType}"></div>
        </div>
        
        <a href="/" class="back-link">Generate Another Story</a>
    </div>
</body>
</html>
```

**模板功能:**

1. **Thymeleaf 整合**: 使用 `th:` 屬性進行動態內容處理
2. **響應式設計**: CSS 樣式適配手機和桌面
3. **錯誤處理**: 向使用者顯示驗證錯誤
4. **客戶端處理**: 使用 JavaScript 進行圖片分析 (基於 Transformers.js)

### 5. 配置

**檔案:** `application.properties`

應用程式的配置設定：

```properties
spring.application.name=pet-story-app

# File upload limits
spring.servlet.multipart.max-file-size=10MB
spring.servlet.multipart.max-request-size=10MB

# Logging configuration
logging.level.com.example.petstory=INFO

# GitHub Models configuration
github.models.endpoint=https://models.github.ai/inference
github.models.model=openai/gpt-4.1-nano
```

**配置說明:**

1. **檔案上傳**: 允許最大 10MB 的圖片
2. **日誌記錄**: 控制執行期間記錄的資訊
3. **GitHub Models**: 指定使用的 AI 模型和端點
4. **安全性**: 錯誤處理配置以避免暴露敏感資訊

## 運行應用程式

### 步驟 1: 設置 GitHub Token

首先，您需要將 GitHub Token 設置為環境變數：

**Windows (命令提示字元):**
```cmd
set GITHUB_TOKEN=your_github_token_here
```

**Windows (PowerShell):**
```powershell
$env:GITHUB_TOKEN="your_github_token_here"
```

**Linux/macOS:**
```bash
export GITHUB_TOKEN=your_github_token_here
```

**為什麼需要這樣做:**
- GitHub Models 需要身份驗證才能訪問 AI 模型
- 使用環境變數可避免將敏感 Token 存入原始碼
- `models:read` 權限提供 AI 推理的訪問權限

### 步驟 2: 建置並運行

進入專案目錄：
```bash
cd 04-PracticalSamples/petstory
```

建置應用程式：
```bash
mvn clean compile
```

啟動伺服器：
```bash
mvn spring-boot:run
```

應用程式將在 `http://localhost:8080` 上啟動。

### 步驟 3: 測試應用程式

1. **打開**瀏覽器並進入 `http://localhost:8080`
2. **描述**您的寵物 (例如: "一隻喜歡撿球的活潑金毛")
3. **點擊**"生成故事" 按鈕以獲取 AI 生成的故事
4. **或者**上傳寵物圖片以自動生成描述
5. **查看**根據寵物描述生成的創意故事

## 整體運作方式

以下是生成寵物故事的完整流程：

1. **使用者輸入**: 您在網頁表單中描述您的寵物
2. **表單提交**: 瀏覽器向 `/generate-story` 發送 POST 請求
3. **控制器處理**: `PetController` 驗證並清理輸入
4. **AI 服務調用**: `StoryService` 向 GitHub Models API 發送請求
5. **故事生成**: AI 根據描述生成創意故事
6. **響應處理**: 控制器接收故事並將其添加到模型
7. **模板渲染**: Thymeleaf 使用故事渲染 `result.html`
8. **展示**: 使用者在瀏覽器中看到生成的故事

**錯誤處理流程:**
如果 AI 服務失敗：
1. 控制器捕捉例外
2. 使用預先撰寫的模板生成備用故事
3. 顯示備用故事並附上 AI 不可用的提示
4. 確保使用者仍然能獲得故事，提供良好的使用者體驗

## 了解 AI 整合

### GitHub Models API
應用程式使用 GitHub Models，提供免費訪問各種 AI 模型：

```java
// Authentication with GitHub token
this.openAIClient = OpenAIOkHttpClient.builder()
    .baseUrl("https://models.github.ai/inference")
    .apiKey(githubToken)
    .build();
```

### 提示工程
服務使用精心設計的提示以獲得良好的結果：

```java
String systemPrompt = "You are a creative storyteller who writes fun, " +
                     "family-friendly short stories about pets. " +
                     "Keep stories under 500 words and appropriate for all ages.";
```

### 響應處理
AI 的響應會被提取並驗證：

```java
ChatCompletion response = openAIClient.chat().completions().create(params);
String story = response.choices().get(0).message().content().orElse("");
```

## 下一步

更多範例請參考 [第 04 章: 實用範例](../README.md)

**免責聲明**：  
本文件已使用 AI 翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 進行翻譯。雖然我們努力確保翻譯的準確性，但請注意，自動翻譯可能包含錯誤或不準確之處。原始文件的母語版本應被視為權威來源。對於關鍵信息，建議使用專業人工翻譯。我們對因使用此翻譯而引起的任何誤解或誤釋不承擔責任。