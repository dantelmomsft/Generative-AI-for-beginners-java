<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "40abf4889418bff189039ac30ff44281",
  "translation_date": "2025-07-23T12:06:13+00:00",
  "source_file": "02-SetupDevEnvironment/README.md",
  "language_code": "hi"
}
-->
# जेनरेटिव एआई के लिए जावा डेवलपमेंट एनवायरनमेंट सेटअप करना

> **त्वरित शुरुआत**: क्लाउड में कोडिंग शुरू करें सिर्फ 2 मिनट में - [GitHub Codespaces Setup](../../../02-SetupDevEnvironment) पर जाएं - कोई लोकल इंस्टॉलेशन की आवश्यकता नहीं है और यह GitHub मॉडल्स का उपयोग करता है!

> **Azure OpenAI में रुचि है?** [Azure OpenAI Setup Guide](getting-started-azure-openai.md) देखें, जिसमें नया Azure OpenAI संसाधन बनाने के चरण शामिल हैं।

## आप क्या सीखेंगे

- एआई एप्लिकेशन के लिए जावा डेवलपमेंट एनवायरनमेंट सेटअप करना
- अपनी पसंद का डेवलपमेंट एनवायरनमेंट चुनना और कॉन्फ़िगर करना (Codespaces के साथ क्लाउड-फर्स्ट, लोकल डेव कंटेनर, या पूरी तरह से लोकल सेटअप)
- GitHub मॉडल्स से कनेक्ट करके अपने सेटअप का परीक्षण करना

## सामग्री की सूची

- [आप क्या सीखेंगे](../../../02-SetupDevEnvironment)
- [परिचय](../../../02-SetupDevEnvironment)
- [चरण 1: अपना डेवलपमेंट एनवायरनमेंट सेट करें](../../../02-SetupDevEnvironment)
  - [विकल्प A: GitHub Codespaces (अनुशंसित)](../../../02-SetupDevEnvironment)
  - [विकल्प B: लोकल डेव कंटेनर](../../../02-SetupDevEnvironment)
  - [विकल्प C: अपने मौजूदा लोकल इंस्टॉलेशन का उपयोग करें](../../../02-SetupDevEnvironment)
- [चरण 2: GitHub पर्सनल एक्सेस टोकन बनाएं](../../../02-SetupDevEnvironment)
- [चरण 3: अपने सेटअप का परीक्षण करें](../../../02-SetupDevEnvironment)
- [समस्या निवारण](../../../02-SetupDevEnvironment)
- [सारांश](../../../02-SetupDevEnvironment)
- [अगले कदम](../../../02-SetupDevEnvironment)

## परिचय

यह अध्याय आपको डेवलपमेंट एनवायरनमेंट सेटअप करने में मार्गदर्शन करेगा। हम **GitHub मॉडल्स** का उपयोग करेंगे क्योंकि यह मुफ़्त है, केवल एक GitHub खाते के साथ सेटअप करना आसान है, क्रेडिट कार्ड की आवश्यकता नहीं है, और प्रयोग के लिए कई मॉडल्स तक पहुंच प्रदान करता है।

**कोई लोकल सेटअप की आवश्यकता नहीं!** आप तुरंत कोडिंग शुरू कर सकते हैं GitHub Codespaces का उपयोग करके, जो आपके ब्राउज़र में एक पूर्ण डेवलपमेंट एनवायरनमेंट प्रदान करता है।

<img src="./images/models.webp" alt="स्क्रीनशॉट: GitHub मॉडल्स" width="50%">

हम इस कोर्स के लिए [**GitHub मॉडल्स**](https://github.com/marketplace?type=models) का उपयोग करने की अनुशंसा करते हैं क्योंकि यह:
- **मुफ़्त** है शुरू करने के लिए
- **आसान** है केवल एक GitHub खाते के साथ सेटअप करने के लिए
- **क्रेडिट कार्ड** की आवश्यकता नहीं है
- **कई मॉडल्स** प्रयोग के लिए उपलब्ध हैं

> **नोट**: इस प्रशिक्षण में उपयोग किए गए GitHub मॉडल्स के मुफ़्त उपयोग की सीमाएँ हैं:
> - प्रति मिनट 15 अनुरोध (प्रति दिन 150)
> - ~8,000 शब्द इनपुट, ~4,000 शब्द आउटपुट प्रति अनुरोध
> - 5 समवर्ती अनुरोध
> 
> प्रोडक्शन उपयोग के लिए, अपने Azure खाते के साथ Azure AI Foundry मॉडल्स में अपग्रेड करें। आपके कोड को बदलने की आवश्यकता नहीं है। [Azure AI Foundry दस्तावेज़](https://learn.microsoft.com/azure/ai-foundry/foundry-models/how-to/quickstart-github-models) देखें।

## चरण 1: अपना डेवलपमेंट एनवायरनमेंट सेट करें

<a name="quick-start-cloud"></a>

हमने इस जेनरेटिव एआई फॉर जावा कोर्स के लिए आवश्यक सभी टूल्स के साथ एक प्री-कॉन्फ़िगर किया हुआ डेवलपमेंट कंटेनर बनाया है ताकि सेटअप समय को कम किया जा सके। अपनी पसंद का डेवलपमेंट तरीका चुनें:

### एनवायरनमेंट सेटअप विकल्प:

#### विकल्प A: GitHub Codespaces (अनुशंसित)

**सिर्फ 2 मिनट में कोडिंग शुरू करें - कोई लोकल सेटअप की आवश्यकता नहीं!**

1. इस रिपॉजिटरी को अपने GitHub खाते में फोर्क करें
   > **नोट**: यदि आप बेसिक कॉन्फ़िगरेशन को संपादित करना चाहते हैं, तो [Dev Container Configuration](../../../.devcontainer/devcontainer.json) देखें।
2. **Code** → **Codespaces** टैब → **...** → **New with options...** पर क्लिक करें।
3. डिफ़ॉल्ट विकल्पों का उपयोग करें – यह **Generative AI Java Development Environment** कस्टम डेवकंटेनर का चयन करेगा, जो इस कोर्स के लिए बनाया गया है।
4. **Create codespace** पर क्लिक करें।
5. ~2 मिनट प्रतीक्षा करें जब तक एनवायरनमेंट तैयार न हो जाए।
6. [चरण 2: GitHub टोकन बनाएं](../../../02-SetupDevEnvironment) पर आगे बढ़ें।

<img src="./images/codespaces.png" alt="स्क्रीनशॉट: Codespaces सबमेनू" width="50%">

<img src="./images/image.png" alt="स्क्रीनशॉट: New with options" width="50%">

<img src="./images/codespaces-create.png" alt="स्क्रीनशॉट: Create codespace options" width="50%">

> **Codespaces के लाभ**:
> - कोई लोकल इंस्टॉलेशन की आवश्यकता नहीं
> - किसी भी डिवाइस पर ब्राउज़र के साथ काम करता है
> - सभी टूल्स और डिपेंडेंसीज़ के साथ प्री-कॉन्फ़िगर
> - व्यक्तिगत खातों के लिए प्रति माह 60 घंटे मुफ़्त
> - सभी शिक्षार्थियों के लिए एक समान एनवायरनमेंट

#### विकल्प B: लोकल डेव कंटेनर

**उन डेवलपर्स के लिए जो Docker के साथ लोकल डेवलपमेंट पसंद करते हैं**

1. इस रिपॉजिटरी को अपने लोकल मशीन पर फोर्क और क्लोन करें।
   > **नोट**: यदि आप बेसिक कॉन्फ़िगरेशन को संपादित करना चाहते हैं, तो [Dev Container Configuration](../../../.devcontainer/devcontainer.json) देखें।
2. [Docker Desktop](https://www.docker.com/products/docker-desktop/) और [VS Code](https://code.visualstudio.com/) इंस्टॉल करें।
3. VS Code में [Dev Containers एक्सटेंशन](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) इंस्टॉल करें।
4. रिपॉजिटरी फ़ोल्डर को VS Code में खोलें।
5. जब संकेत दिया जाए, तो **Reopen in Container** पर क्लिक करें (या `Ctrl+Shift+P` → "Dev Containers: Reopen in Container" का उपयोग करें)।
6. कंटेनर के बनने और शुरू होने की प्रतीक्षा करें।
7. [चरण 2: GitHub टोकन बनाएं](../../../02-SetupDevEnvironment) पर आगे बढ़ें।

<img src="./images/devcontainer.png" alt="स्क्रीनशॉट: Dev container setup" width="50%">

<img src="./images/image-3.png" alt="स्क्रीनशॉट: Dev container build complete" width="50%">

#### विकल्प C: अपने मौजूदा लोकल इंस्टॉलेशन का उपयोग करें

**उन डेवलपर्स के लिए जिनके पास पहले से जावा एनवायरनमेंट है**

पूर्वापेक्षाएँ:
- [Java 21+](https://www.oracle.com/java/technologies/javase/jdk21-archive-downloads.html) 
- [Maven 3.9+](https://maven.apache.org/download.cgi)
- [VS Code](https://code.visualstudio.com) या आपका पसंदीदा IDE

चरण:
1. इस रिपॉजिटरी को अपने लोकल मशीन पर क्लोन करें।
2. प्रोजेक्ट को अपने IDE में खोलें।
3. [चरण 2: GitHub टोकन बनाएं](../../../02-SetupDevEnvironment) पर आगे बढ़ें।

> **प्रो टिप**: यदि आपके पास लो-स्पेक मशीन है लेकिन आप लोकल VS Code चाहते हैं, तो GitHub Codespaces का उपयोग करें! आप अपने लोकल VS Code को क्लाउड-होस्टेड Codespace से कनेक्ट कर सकते हैं और दोनों का लाभ उठा सकते हैं।

<img src="./images/image-2.png" alt="स्क्रीनशॉट: created local devcontainer instance" width="50%">

## चरण 2: GitHub पर्सनल एक्सेस टोकन बनाएं

1. [GitHub Settings](https://github.com/settings/profile) पर जाएं और अपने प्रोफाइल मेनू से **Settings** चुनें।
2. बाईं साइडबार में, **Developer settings** पर क्लिक करें (आमतौर पर सबसे नीचे)।
3. **Personal access tokens** के तहत, **Fine-grained tokens** पर क्लिक करें (या इस [लिंक](https://github.com/settings/personal-access-tokens) का अनुसरण करें)।
4. **Generate new token** पर क्लिक करें।
5. "Token name" के तहत, एक वर्णनात्मक नाम दें (जैसे, `GenAI-Java-Course-Token`)।
6. समाप्ति तिथि सेट करें (सुरक्षा के लिए अनुशंसित: 7 दिन)।
7. "Resource owner" के तहत, अपना उपयोगकर्ता खाता चुनें।
8. "Repository access" के तहत, उन रिपॉजिटरीज़ को चुनें जिन्हें आप GitHub मॉडल्स के साथ उपयोग करना चाहते हैं (या "All repositories" यदि आवश्यक हो)।
9. "Repository permissions" के तहत, **Models** खोजें और इसे **Read and write** पर सेट करें।
10. **Generate token** पर क्लिक करें।
11. **अभी अपना टोकन कॉपी और सेव करें** – आप इसे फिर से नहीं देख पाएंगे!

> **सुरक्षा टिप**: अपने एक्सेस टोकन के लिए न्यूनतम आवश्यक स्कोप और सबसे कम व्यावहारिक समाप्ति समय का उपयोग करें।

## चरण 3: GitHub मॉडल्स उदाहरण के साथ अपने सेटअप का परीक्षण करें

एक बार आपका डेवलपमेंट एनवायरनमेंट तैयार हो जाए, तो चलिए GitHub मॉडल्स इंटीग्रेशन को हमारे उदाहरण एप्लिकेशन के साथ परीक्षण करते हैं [`02-SetupDevEnvironment/src/github-models`](../../../02-SetupDevEnvironment/src/github-models)।

1. अपने डेवलपमेंट एनवायरनमेंट में टर्मिनल खोलें।
2. GitHub मॉडल्स उदाहरण पर जाएं:
   ```bash
   cd 02-SetupDevEnvironment/src/github-models
   ```
3. अपने GitHub टोकन को एक एनवायरनमेंट वेरिएबल के रूप में सेट करें:
   ```bash
   # macOS/Linux
   export GITHUB_TOKEN=your_token_here
   
   # Windows (Command Prompt)
   set GITHUB_TOKEN=your_token_here
   
   # Windows (PowerShell)
   $env:GITHUB_TOKEN="your_token_here"
   ```

4. एप्लिकेशन चलाएं:
   ```bash
   mvn compile exec:java -Dexec.mainClass="com.example.githubmodels.App"
   ```

आपको इस तरह का आउटपुट दिखाई देना चाहिए:
```text
Using model: gpt-4.1-nano
Sending request to GitHub Models...
Response: Hello World!
```

### उदाहरण कोड को समझना

पहले, चलिए समझते हैं कि आपने अभी क्या चलाया। `src/github-models` के तहत उदाहरण OpenAI Java SDK का उपयोग करता है GitHub मॉडल्स से कनेक्ट करने के लिए:

**यह कोड क्या करता है:**
- GitHub मॉडल्स से **कनेक्ट** करता है आपके पर्सनल एक्सेस टोकन का उपयोग करके
- एआई मॉडल को एक साधारण "Say Hello World!" संदेश **भेजता** है
- एआई का उत्तर **प्राप्त** करता है और प्रदर्शित करता है
- आपके सेटअप को सही ढंग से काम कर रहा है यह **सत्यापित** करता है

**मुख्य डिपेंडेंसी** (`pom.xml` में):
```xml
<dependency>
    <groupId>com.openai</groupId>
    <artifactId>openai-java</artifactId>
    <version>2.12.0</version>
</dependency>
```

**मुख्य कोड** (`App.java`):
```java
// Connect to GitHub Models using OpenAI Java SDK
OpenAIClient client = OpenAIOkHttpClient.builder()
    .apiKey(pat)
    .baseUrl("https://models.inference.ai.azure.com")
    .build();

// Create chat completion request
ChatCompletionCreateParams params = ChatCompletionCreateParams.builder()
    .model(modelId)
    .addSystemMessage("You are a concise assistant.")
    .addUserMessage("Say Hello World!")
    .build();

// Get AI response
ChatCompletion response = client.chat().completions().create(params);
System.out.println("Response: " + response.choices().get(0).message().content().orElse("No response content"));
```

## सारांश

**बधाई हो!** आपने सफलतापूर्वक:

- **GitHub पर्सनल एक्सेस टोकन बनाया** एआई मॉडल एक्सेस के लिए उचित अनुमतियों के साथ
- **जावा डेवलपमेंट एनवायरनमेंट सेटअप किया** Codespaces, डेव कंटेनर्स, या लोकल इंस्टॉलेशन का उपयोग करके
- **GitHub मॉडल्स से कनेक्ट किया** OpenAI Java SDK का उपयोग करके मुफ़्त एआई डेवलपमेंट एक्सेस के लिए
- **इंटीग्रेशन का परीक्षण किया** एक कार्यशील उदाहरण एप्लिकेशन के साथ जो एआई मॉडल्स के साथ संवाद करता है

## अगले कदम

[अध्याय 3: कोर जेनरेटिव एआई तकनीकें](../03-CoreGenerativeAITechniques/README.md)

## समस्या निवारण

समस्याएँ आ रही हैं? यहाँ सामान्य समस्याएँ और उनके समाधान दिए गए हैं:

- **टोकन काम नहीं कर रहा?** 
  - सुनिश्चित करें कि आपने पूरा टोकन बिना किसी अतिरिक्त स्पेस के कॉपी किया है
  - सत्यापित करें कि टोकन सही ढंग से एनवायरनमेंट वेरिएबल के रूप में सेट है
  - जांचें कि आपके टोकन में सही अनुमतियाँ हैं (Models: Read and write)

- **Maven नहीं मिला?** 
  - यदि आप डेव कंटेनर्स/Codespaces का उपयोग कर रहे हैं, तो Maven पहले से इंस्टॉल होना चाहिए
  - लोकल सेटअप के लिए, सुनिश्चित करें कि Java 21+ और Maven 3.9+ इंस्टॉल हैं
  - `mvn --version` चलाकर इंस्टॉलेशन सत्यापित करें

- **कनेक्शन समस्याएँ?** 
  - अपना इंटरनेट कनेक्शन जांचें
  - सत्यापित करें कि GitHub आपके नेटवर्क से सुलभ है
  - सुनिश्चित करें कि आप किसी फ़ायरवॉल के पीछे नहीं हैं जो GitHub मॉडल्स एंडपॉइंट को ब्लॉक कर रहा है

- **डेव कंटेनर शुरू नहीं हो रहा?** 
  - सुनिश्चित करें कि Docker Desktop चल रहा है (लोकल डेवलपमेंट के लिए)
  - कंटेनर को फिर से बनाने का प्रयास करें: `Ctrl+Shift+P` → "Dev Containers: Rebuild Container"

- **एप्लिकेशन संकलन त्रुटियाँ?**
  - सुनिश्चित करें कि आप सही डायरेक्टरी में हैं: `02-SetupDevEnvironment/src/github-models`
  - साफ़ करने और फिर से बनाने का प्रयास करें: `mvn clean compile`

> **मदद चाहिए?**: अभी भी समस्याएँ आ रही हैं? रिपॉजिटरी में एक इश्यू खोलें और हम आपकी मदद करेंगे।

**अस्वीकरण**:  
यह दस्तावेज़ AI अनुवाद सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) का उपयोग करके अनुवादित किया गया है। जबकि हम सटीकता सुनिश्चित करने का प्रयास करते हैं, कृपया ध्यान दें कि स्वचालित अनुवाद में त्रुटियां या अशुद्धियां हो सकती हैं। मूल भाषा में उपलब्ध मूल दस्तावेज़ को आधिकारिक स्रोत माना जाना चाहिए। महत्वपूर्ण जानकारी के लिए, पेशेवर मानव अनुवाद की सिफारिश की जाती है। इस अनुवाद के उपयोग से उत्पन्न किसी भी गलतफहमी या गलत व्याख्या के लिए हम जिम्मेदार नहीं हैं।