<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "59454ab4ec36d89840df6fcfe7633cbd",
  "translation_date": "2025-07-25T10:46:23+00:00",
  "source_file": "03-CoreGenerativeAITechniques/README.md",
  "language_code": "fa"
}
-->
# آموزش تکنیک‌های اصلی هوش مصنوعی مولد

## فهرست مطالب

- [پیش‌نیازها](../../../03-CoreGenerativeAITechniques)
- [شروع به کار](../../../03-CoreGenerativeAITechniques)
  - [مرحله ۱: تنظیم متغیر محیطی](../../../03-CoreGenerativeAITechniques)
  - [مرحله ۲: رفتن به دایرکتوری مثال‌ها](../../../03-CoreGenerativeAITechniques)
- [آموزش ۱: تکمیل‌ها و چت با LLM](../../../03-CoreGenerativeAITechniques)
- [آموزش ۲: فراخوانی توابع](../../../03-CoreGenerativeAITechniques)
- [آموزش ۳: RAG (تولید تقویت‌شده با بازیابی)](../../../03-CoreGenerativeAITechniques)
- [آموزش ۴: هوش مصنوعی مسئولانه](../../../03-CoreGenerativeAITechniques)
- [الگوهای مشترک در مثال‌ها](../../../03-CoreGenerativeAITechniques)
- [گام‌های بعدی](../../../03-CoreGenerativeAITechniques)
- [رفع اشکال](../../../03-CoreGenerativeAITechniques)
  - [مشکلات رایج](../../../03-CoreGenerativeAITechniques)

## مرور کلی

این آموزش شامل مثال‌های عملی از تکنیک‌های اصلی هوش مصنوعی مولد با استفاده از جاوا و مدل‌های GitHub است. شما یاد خواهید گرفت که چگونه با مدل‌های زبانی بزرگ (LLM) تعامل داشته باشید، فراخوانی توابع را پیاده‌سازی کنید، از تولید تقویت‌شده با بازیابی (RAG) استفاده کنید و اصول هوش مصنوعی مسئولانه را اعمال کنید.

## پیش‌نیازها

قبل از شروع، مطمئن شوید که موارد زیر را دارید:
- نصب جاوا ۲۱ یا بالاتر
- ابزار Maven برای مدیریت وابستگی‌ها
- یک حساب GitHub با یک توکن دسترسی شخصی (PAT)

## شروع به کار

### مرحله ۱: تنظیم متغیر محیطی

ابتدا باید توکن GitHub خود را به‌عنوان یک متغیر محیطی تنظیم کنید. این توکن به شما امکان می‌دهد به مدل‌های GitHub به‌صورت رایگان دسترسی داشته باشید.

**ویندوز (Command Prompt):**
```cmd
set GITHUB_TOKEN=your_github_token_here
```

**ویندوز (PowerShell):**
```powershell
$env:GITHUB_TOKEN="your_github_token_here"
```

**لینوکس/macOS:**
```bash
export GITHUB_TOKEN=your_github_token_here
```

### مرحله ۲: رفتن به دایرکتوری مثال‌ها

```bash
cd 03-CoreGenerativeAITechniques/examples/
```

## آموزش ۱: تکمیل‌ها و چت با LLM

**فایل:** `src/main/java/com/example/genai/techniques/completions/LLMCompletionsApp.java`

### این مثال چه چیزی آموزش می‌دهد؟

این مثال مکانیک‌های اصلی تعامل با مدل‌های زبانی بزرگ (LLM) از طریق API OpenAI را نشان می‌دهد، از جمله:
- مقداردهی اولیه کلاینت با مدل‌های GitHub
- الگوهای ساختار پیام برای درخواست‌های سیستم و کاربر
- مدیریت وضعیت مکالمه از طریق انباشت تاریخچه پیام‌ها
- تنظیم پارامترها برای کنترل طول پاسخ و سطح خلاقیت

### مفاهیم کلیدی کد

#### ۱. تنظیم کلاینت
```java
// Create the AI client
OpenAIClient client = new OpenAIClientBuilder()
    .endpoint("https://models.inference.ai.azure.com")
    .credential(new StaticTokenCredential(pat))
    .buildClient();
```

این کد اتصال به مدل‌های GitHub را با استفاده از توکن شما ایجاد می‌کند.

#### ۲. تکمیل ساده
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

#### ۳. حافظه مکالمه
```java
// Add AI's response to maintain conversation history
messages.add(new ChatRequestAssistantMessage(aiResponse));
messages.add(new ChatRequestUserMessage("Follow-up question"));
```

مدل تنها در صورتی پیام‌های قبلی را به خاطر می‌آورد که آن‌ها را در درخواست‌های بعدی بگنجانید.

### اجرای مثال
```bash
mvn compile exec:java -Dexec.mainClass="com.example.genai.techniques.completions.LLMCompletionsApp"
```

### چه اتفاقی می‌افتد وقتی آن را اجرا می‌کنید؟

1. **تکمیل ساده**: مدل به یک سؤال جاوا با راهنمایی درخواست سیستم پاسخ می‌دهد.
2. **چت چندمرحله‌ای**: مدل زمینه را در چندین سؤال حفظ می‌کند.
3. **چت تعاملی**: می‌توانید یک مکالمه واقعی با مدل داشته باشید.

## آموزش ۲: فراخوانی توابع

**فایل:** `src/main/java/com/example/genai/techniques/functions/FunctionsApp.java`

### این مثال چه چیزی آموزش می‌دهد؟

فراخوانی توابع به مدل‌های هوش مصنوعی امکان می‌دهد درخواست اجرای ابزارها و APIهای خارجی را از طریق یک پروتکل ساختاریافته ارائه دهند. مدل درخواست‌های زبان طبیعی را تحلیل می‌کند، فراخوانی‌های توابع موردنیاز را با پارامترهای مناسب بر اساس تعریف JSON Schema تعیین می‌کند و نتایج بازگشتی را برای تولید پاسخ‌های متنی پردازش می‌کند، در حالی که اجرای واقعی توابع برای امنیت و قابلیت اطمینان تحت کنترل توسعه‌دهنده باقی می‌ماند.

### مفاهیم کلیدی کد

#### ۱. تعریف تابع
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

این کد به مدل می‌گوید چه توابعی در دسترس هستند و چگونه از آن‌ها استفاده کند.

#### ۲. جریان اجرای تابع
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

#### ۳. پیاده‌سازی تابع
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

### اجرای مثال
```bash
mvn compile exec:java -Dexec.mainClass="com.example.genai.techniques.functions.FunctionsApp"
```

### چه اتفاقی می‌افتد وقتی آن را اجرا می‌کنید؟

1. **تابع آب‌وهوا**: مدل درخواست داده‌های آب‌وهوای سیاتل را می‌دهد، شما آن را فراهم می‌کنید، مدل پاسخ را قالب‌بندی می‌کند.
2. **تابع ماشین‌حساب**: مدل درخواست محاسبه (۱۵٪ از ۲۴۰) را می‌دهد، شما آن را محاسبه می‌کنید، مدل نتیجه را توضیح می‌دهد.

## آموزش ۳: RAG (تولید تقویت‌شده با بازیابی)

**فایل:** `src/main/java/com/example/genai/techniques/rag/SimpleReaderDemo.java`

### این مثال چه چیزی آموزش می‌دهد؟

تولید تقویت‌شده با بازیابی (RAG) ترکیبی از بازیابی اطلاعات و تولید زبان است. این روش با تزریق محتوای اسناد خارجی به درخواست‌های مدل، به مدل‌ها امکان می‌دهد پاسخ‌های دقیق بر اساس منابع دانش خاص ارائه دهند، در حالی که مرزهای واضحی بین پرسش‌های کاربر و منابع اطلاعات معتبر از طریق مهندسی استراتژیک درخواست‌ها حفظ می‌شود.

### مفاهیم کلیدی کد

#### ۱. بارگذاری اسناد
```java
// Load your knowledge source
String doc = Files.readString(Paths.get("document.txt"));
```

#### ۲. تزریق زمینه
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

علامت‌های نقل قول سه‌گانه به مدل کمک می‌کنند بین زمینه و سؤال تمایز قائل شود.

#### ۳. مدیریت ایمن پاسخ‌ها
```java
if (response != null && response.getChoices() != null && !response.getChoices().isEmpty()) {
    String answer = response.getChoices().get(0).getMessage().getContent();
    System.out.println("Assistant: " + answer);
} else {
    System.err.println("Error: No response received from the API.");
}
```

همیشه پاسخ‌های API را برای جلوگیری از خرابی اعتبارسنجی کنید.

### اجرای مثال
```bash
mvn compile exec:java -Dexec.mainClass="com.example.genai.techniques.rag.SimpleReaderDemo"
```

### چه اتفاقی می‌افتد وقتی آن را اجرا می‌کنید؟

1. برنامه فایل `document.txt` را بارگذاری می‌کند (حاوی اطلاعاتی درباره مدل‌های GitHub است).
2. شما سؤالی درباره سند می‌پرسید.
3. مدل فقط بر اساس محتوای سند پاسخ می‌دهد، نه دانش عمومی خود.

سعی کنید بپرسید: "مدل‌های GitHub چیست؟" در مقابل "هوا چگونه است؟"

## آموزش ۴: هوش مصنوعی مسئولانه

**فایل:** `src/main/java/com/example/genai/techniques/responsibleai/ResponsibleGithubModels.java`

### این مثال چه چیزی آموزش می‌دهد؟

این مثال اهمیت پیاده‌سازی اقدامات ایمنی در برنامه‌های هوش مصنوعی را نشان می‌دهد. این مثال فیلترهای ایمنی را نمایش می‌دهد که دسته‌های محتوای مضر از جمله سخنان نفرت‌انگیز، آزار و اذیت، خودآزاری، محتوای جنسی و خشونت را شناسایی می‌کنند. همچنین نشان می‌دهد که چگونه برنامه‌های هوش مصنوعی تولیدی باید نقض سیاست محتوا را از طریق مدیریت استثناها، مکانیزم‌های بازخورد کاربر و استراتژی‌های پاسخ جایگزین به‌طور مناسب مدیریت کنند.

### مفاهیم کلیدی کد

#### ۱. چارچوب تست ایمنی
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

#### ۲. دسته‌های ایمنی مورد آزمایش
- دستورالعمل‌های خشونت/آسیب
- سخنان نفرت‌انگیز
- نقض حریم خصوصی
- اطلاعات نادرست پزشکی
- فعالیت‌های غیرقانونی

### اجرای مثال
```bash
mvn compile exec:java -Dexec.mainClass="com.example.genai.techniques.responsibleai.ResponsibleGithubModels"
```

### چه اتفاقی می‌افتد وقتی آن را اجرا می‌کنید؟

برنامه درخواست‌های مضر مختلف را آزمایش می‌کند و نشان می‌دهد که سیستم ایمنی هوش مصنوعی چگونه:
1. **درخواست‌های خطرناک را مسدود می‌کند** با خطاهای HTTP 400
2. **محتوای ایمن را به‌طور عادی تولید می‌کند**
3. **کاربران را از خروجی‌های مضر هوش مصنوعی محافظت می‌کند**

## الگوهای مشترک در مثال‌ها

### الگوی احراز هویت
تمام مثال‌ها از این الگو برای احراز هویت با مدل‌های GitHub استفاده می‌کنند:

```java
String pat = System.getenv("GITHUB_TOKEN");
TokenCredential credential = new StaticTokenCredential(pat);
OpenAIClient client = new OpenAIClientBuilder()
    .endpoint("https://models.inference.ai.azure.com")
    .credential(credential)
    .buildClient();
```

### الگوی مدیریت خطا
```java
try {
    // AI operation
} catch (HttpResponseException e) {
    // Handle API errors (rate limits, safety filters)
} catch (Exception e) {
    // Handle general errors (network, parsing)
}
```

### الگوی ساختار پیام
```java
List<ChatRequestMessage> messages = List.of(
    new ChatRequestSystemMessage("Set AI behavior"),
    new ChatRequestUserMessage("User's actual request")
);
```

## گام‌های بعدی

[فصل ۰۴: نمونه‌های عملی](../04-PracticalSamples/README.md)

## رفع اشکال

### مشکلات رایج

**"GITHUB_TOKEN تنظیم نشده است"**
- مطمئن شوید که متغیر محیطی را تنظیم کرده‌اید.
- بررسی کنید که توکن شما دارای محدوده `models:read` باشد.

**"هیچ پاسخی از API دریافت نشد"**
- اتصال اینترنت خود را بررسی کنید.
- مطمئن شوید که توکن شما معتبر است.
- بررسی کنید که آیا به محدودیت‌های نرخ دسترسی رسیده‌اید.

**خطاهای کامپایل Maven**
- مطمئن شوید که جاوا ۲۱ یا بالاتر را نصب کرده‌اید.
- دستور `mvn clean compile` را برای به‌روزرسانی وابستگی‌ها اجرا کنید.

**سلب مسئولیت**:  
این سند با استفاده از سرویس ترجمه هوش مصنوعی [Co-op Translator](https://github.com/Azure/co-op-translator) ترجمه شده است. در حالی که ما تلاش می‌کنیم دقت را حفظ کنیم، لطفاً توجه داشته باشید که ترجمه‌های خودکار ممکن است شامل خطاها یا نادرستی‌ها باشند. سند اصلی به زبان اصلی آن باید به عنوان منبع معتبر در نظر گرفته شود. برای اطلاعات حیاتی، ترجمه حرفه‌ای انسانی توصیه می‌شود. ما مسئولیتی در قبال سوء تفاهم‌ها یا تفسیرهای نادرست ناشی از استفاده از این ترجمه نداریم.