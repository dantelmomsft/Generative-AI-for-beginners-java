<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "a49b35508745c032a0033d914df7901b",
  "translation_date": "2025-07-25T09:16:45+00:00",
  "source_file": "README.md",
  "language_code": "pa"
}
-->
# ਜਨਰੇਟਿਵ ਏਆਈ ਸ਼ੁਰੂਆਤੀਆਂ ਲਈ - ਜਾਵਾ ਐਡੀਸ਼ਨ
[![Microsoft Azure AI Foundry Discord](https://dcbadge.limes.pink/api/server/ByRwuEEgH4)](https://discord.com/invite/ByRwuEEgH4)

![ਜਨਰੇਟਿਵ ਏਆਈ ਸ਼ੁਰੂਆਤੀਆਂ ਲਈ - ਜਾਵਾ ਐਡੀਸ਼ਨ](../../translated_images/beg-genai-series.61edc4a6b2cc54284fa2d70eda26dc0ca2669e26e49655b842ea799cd6e16d2a.pa.png)

**ਸਮਾਂ ਦੀ ਲੋੜ**: ਪੂਰਾ ਵਰਕਸ਼ਾਪ ਆਨਲਾਈਨ ਬਿਨਾਂ ਕਿਸੇ ਲੋਕਲ ਸੈਟਅੱਪ ਦੇ ਪੂਰਾ ਕੀਤਾ ਜਾ ਸਕਦਾ ਹੈ। ਜੇ ਤੁਸੀਂ ਸੈਂਪਲ ਚਲਾਉਣਾ ਚਾਹੁੰਦੇ ਹੋ, ਤਾਂ ਵਾਤਾਵਰਣ ਸੈਟਅੱਪ ਕਰਨ ਵਿੱਚ 2 ਮਿੰਟ ਲੱਗਦੇ ਹਨ, ਅਤੇ ਸੈਂਪਲ ਦੀ ਖੋਜ ਕਰਨ ਵਿੱਚ 1-3 ਘੰਟੇ ਲੱਗ ਸਕਦੇ ਹਨ, ਖੋਜ ਦੀ ਗਹਿਰਾਈ 'ਤੇ ਨਿਰਭਰ ਕਰਦਾ ਹੈ।

> **ਤੁਰੰਤ ਸ਼ੁਰੂਆਤ**

1. ਇਸ ਰਿਪੋਜ਼ਟਰੀ ਨੂੰ ਆਪਣੇ GitHub ਖਾਤੇ 'ਤੇ ਫੋਰਕ ਕਰੋ
2. **Code** → **Codespaces** ਟੈਬ → **...** → **New with options...** 'ਤੇ ਕਲਿਕ ਕਰੋ
3. ਡਿਫਾਲਟ ਸੈਟਿੰਗਾਂ ਵਰਤੋ – ਇਹ ਇਸ ਕੋਰਸ ਲਈ ਬਣਾਏ ਗਏ ਡਿਵੈਲਪਮੈਂਟ ਕੰਟੇਨਰ ਨੂੰ ਚੁਣੇਗਾ
4. **Create codespace** 'ਤੇ ਕਲਿਕ ਕਰੋ
5. ਵਾਤਾਵਰਣ ਤਿਆਰ ਹੋਣ ਲਈ ~2 ਮਿੰਟ ਇੰਤਜ਼ਾਰ ਕਰੋ
6. ਸਿੱਧੇ [ਆਪਣਾ GitHub ਮਾਡਲ ਟੋਕਨ ਬਣਾਉਣ](./02-SetupDevEnvironment/README.md#step-2-create-a-github-personal-access-token) 'ਤੇ ਜਾਓ

## ਬਹੁ-ਭਾਸ਼ਾਈ ਸਹਾਇਤਾ

### GitHub Action ਰਾਹੀਂ ਸਹਾਇਕ (ਆਟੋਮੈਟਿਕ ਅਤੇ ਹਮੇਸ਼ਾ ਅਪ-ਟੂ-ਡੇਟ)

[ਫਰੈਂਚ](../fr/README.md) | [ਸਪੈਨਿਸ਼](../es/README.md) | [ਜਰਮਨ](../de/README.md) | [ਰੂਸੀ](../ru/README.md) | [ਅਰਬੀ](../ar/README.md) | [ਫ਼ਾਰਸੀ (ਪਰਸੀਅਨ)](../fa/README.md) | [ਉਰਦੂ](../ur/README.md) | [ਚੀਨੀ (ਸਰਲ)](../zh/README.md) | [ਚੀਨੀ (ਰਵਾਇਤੀ, ਮਕਾਉ)](../mo/README.md) | [ਚੀਨੀ (ਰਵਾਇਤੀ, ਹਾਂਗਕਾਂਗ)](../hk/README.md) | [ਚੀਨੀ (ਰਵਾਇਤੀ, ਤਾਈਵਾਨ)](../tw/README.md) | [ਜਾਪਾਨੀ](../ja/README.md) | [ਕੋਰੀਅਨ](../ko/README.md) | [ਹਿੰਦੀ](../hi/README.md) | [ਬੰਗਾਲੀ](../bn/README.md) | [ਮਰਾਠੀ](../mr/README.md) | [ਨੇਪਾਲੀ](../ne/README.md) | [ਪੰਜਾਬੀ (ਗੁਰਮੁਖੀ)](./README.md) | [ਪੁਰਤਗਾਲੀ (ਪੁਰਤਗਾਲ)](../pt/README.md) | [ਪੁਰਤਗਾਲੀ (ਬ੍ਰਾਜ਼ੀਲ)](../br/README.md) | [ਇਟਾਲੀਅਨ](../it/README.md) | [ਪੋਲਿਸ਼](../pl/README.md) | [ਤੁਰਕੀ](../tr/README.md) | [ਗ੍ਰੀਕ](../el/README.md) | [ਥਾਈ](../th/README.md) | [ਸਵੀਡਿਸ਼](../sv/README.md) | [ਡੈਨਿਸ਼](../da/README.md) | [ਨਾਰਵੇਜੀਅਨ](../no/README.md) | [ਫਿਨਿਸ਼](../fi/README.md) | [ਡੱਚ](../nl/README.md) | [ਹਿਬਰੂ](../he/README.md) | [ਵਿਯਤਨਾਮੀ](../vi/README.md) | [ਇੰਡੋਨੇਸ਼ੀਆਈ](../id/README.md) | [ਮਲੇ](../ms/README.md) | [ਟੈਗਾਲੋਗ (ਫਿਲੀਪੀਨੋ)](../tl/README.md) | [ਸਵਾਹਿਲੀ](../sw/README.md) | [ਹੰਗਰੀਅਨ](../hu/README.md) | [ਚੈਕ](../cs/README.md) | [ਸਲੋਵਾਕ](../sk/README.md) | [ਰੋਮਾਨੀਅਨ](../ro/README.md) | [ਬੁਲਗਾਰੀਆਈ](../bg/README.md) | [ਸਰਬੀਅਨ (ਸਿਰਿਲਿਕ)](../sr/README.md) | [ਕਰੋਏਸ਼ੀਆਈ](../hr/README.md) | [ਸਲੋਵੇਨੀਆਈ](../sl/README.md) | [ਯੂਕਰੇਨੀਅਨ](../uk/README.md) | [ਬਰਮੀ (ਮਿਆਂਮਾਰ)](../my/README.md)

## ਕੋਰਸ ਦੀ ਬਣਾਵਟ ਅਤੇ ਸਿੱਖਣ ਦਾ ਰਾਹ

### **ਅਧਿਆਇ 1: ਜਨਰੇਟਿਵ ਏਆਈ ਦਾ ਪਰਿਚਯ**
- **ਮੁੱਖ ਧਾਰਨਾਵਾਂ**: ਵੱਡੇ ਭਾਸ਼ਾ ਮਾਡਲਾਂ, ਟੋਕਨ, ਐਮਬੈਡਿੰਗਜ਼, ਅਤੇ ਏਆਈ ਸਮਰੱਥਾਵਾਂ ਨੂੰ ਸਮਝਣਾ
- **ਜਾਵਾ ਏਆਈ ਪਰਿਪੇਖ**: Spring AI ਅਤੇ OpenAI SDKs ਦਾ ਜਾਇਜ਼ਾ
- **ਮਾਡਲ ਕੌਂਟੈਕਸਟ ਪ੍ਰੋਟੋਕੋਲ**: MCP ਅਤੇ ਇਸ ਦੀ ਏਆਈ ਏਜੰਟ ਸੰਚਾਰ ਵਿੱਚ ਭੂਮਿਕਾ
- **ਵਿਵਹਾਰਕ ਐਪਲੀਕੇਸ਼ਨਜ਼**: ਚੈਟਬੋਟ ਅਤੇ ਸਮੱਗਰੀ ਸਿਰਜਣਾ ਵਰਗੇ ਹਕੀਕਤੀ ਦ੍ਰਿਸ਼ਾਂ
- **[→ ਅਧਿਆਇ 1 ਸ਼ੁਰੂ ਕਰੋ](./01-IntroToGenAI/README.md)**

### **ਅਧਿਆਇ 2: ਵਿਕਾਸ ਵਾਤਾਵਰਣ ਸੈਟਅੱਪ**
- **ਮਲਟੀ-ਪ੍ਰੋਵਾਈਡਰ ਸੰਰਚਨਾ**: GitHub ਮਾਡਲ, Azure OpenAI, ਅਤੇ OpenAI ਜਾਵਾ SDK ਇੰਟੀਗ੍ਰੇਸ਼ਨ ਸੈਟਅੱਪ ਕਰੋ
- **Spring Boot + Spring AI**: ਕਾਰੋਬਾਰੀ ਏਆਈ ਐਪਲੀਕੇਸ਼ਨ ਵਿਕਾਸ ਲਈ ਸਭ ਤੋਂ ਵਧੀਆ ਤਰੀਕੇ
- **GitHub ਮਾਡਲ**: ਪ੍ਰੋਟੋਟਾਈਪਿੰਗ ਅਤੇ ਸਿੱਖਣ ਲਈ ਮੁਫ਼ਤ ਏਆਈ ਮਾਡਲ ਪਹੁੰਚ (ਕੋਈ ਕ੍ਰੈਡਿਟ ਕਾਰਡ ਲੋੜੀਂਦਾ ਨਹੀਂ)
- **ਵਿਕਾਸ ਦੇ ਸੰਦ**: Docker ਕੰਟੇਨਰ, VS Code, ਅਤੇ GitHub Codespaces ਸੰਰਚਨਾ
- **[→ ਅਧਿਆਇ 2 ਸ਼ੁਰੂ ਕਰੋ](./02-SetupDevEnvironment/README.md)**

### **ਅਧਿਆਇ 3: ਮੁੱਖ ਜਨਰੇਟਿਵ ਏਆਈ ਤਕਨੀਕਾਂ**
- **ਪ੍ਰੋੰਪਟ ਇੰਜੀਨੀਅਰਿੰਗ**: ਏਆਈ ਮਾਡਲ ਦੇ ਉੱਤਮ ਜਵਾਬਾਂ ਲਈ ਤਕਨੀਕਾਂ
- **ਐਮਬੈਡਿੰਗਜ਼ ਅਤੇ ਵੇਕਟਰ ਓਪਰੇਸ਼ਨਜ਼**: ਸੈਮਾਂਟਿਕ ਖੋਜ ਅਤੇ ਸਮਾਨਤਾ ਮੈਚਿੰਗ ਨੂੰ ਲਾਗੂ ਕਰੋ
- **ਰਿਟਰੀਵਲ-ਅਗਮੈਂਟਡ ਜਨਰੇਸ਼ਨ (RAG)**: ਆਪਣੇ ਡਾਟਾ ਸਰੋਤਾਂ ਨਾਲ ਏਆਈ ਨੂੰ ਜੋੜੋ
- **ਫੰਕਸ਼ਨ ਕਾਲਿੰਗ**: ਕਸਟਮ ਟੂਲ ਅਤੇ ਪਲੱਗਇਨ ਨਾਲ ਏਆਈ ਸਮਰੱਥਾਵਾਂ ਨੂੰ ਵਧਾਓ
- **[→ ਅਧਿਆਇ 3 ਸ਼ੁਰੂ ਕਰੋ](./03-CoreGenerativeAITechniques/README.md)**

### **ਅਧਿਆਇ 4: ਵਿਵਹਾਰਕ ਐਪਲੀਕੇਸ਼ਨ ਅਤੇ ਪ੍ਰੋਜੈਕਟ**
- **ਪੈਟ ਸਟੋਰੀ ਜਨਰੇਟਰ** (`petstory/`): GitHub ਮਾਡਲਾਂ ਨਾਲ ਰਚਨਾਤਮਕ ਸਮੱਗਰੀ ਸਿਰਜਣਾ
- **Foundry Local Demo** (`foundrylocal/`): OpenAI ਜਾਵਾ SDK ਨਾਲ ਲੋਕਲ ਏਆਈ ਮਾਡਲ ਇੰਟੀਗ੍ਰੇਸ਼ਨ
- **MCP ਕੈਲਕੂਲੇਟਰ ਸੇਵਾ** (`mcp/calculator/`): Spring AI ਨਾਲ ਬੁਨਿਆਦੀ ਮਾਡਲ ਕੌਂਟੈਕਸਟ ਪ੍ਰੋਟੋਕੋਲ ਲਾਗੂ ਕਰਨਾ
- **[→ ਅਧਿਆਇ 4 ਸ਼ੁਰੂ ਕਰੋ](./04-PracticalSamples/README.md)**

### **ਅਧਿਆਇ 5: ਜ਼ਿੰਮੇਵਾਰ ਏਆਈ ਵਿਕਾਸ**
- **GitHub ਮਾਡਲ ਸੁਰੱਖਿਆ**: ਅੰਦਰੂਨੀ ਸਮੱਗਰੀ ਫਿਲਟਰੀਕਰਨ ਅਤੇ ਸੁਰੱਖਿਆ ਮਕੈਨਿਜ਼ਮ ਦੀ ਜਾਂਚ ਕਰੋ
- **ਜ਼ਿੰਮੇਵਾਰ ਏਆਈ ਡੈਮੋ**: ਹਕੀਕਤੀ ਉਦਾਹਰਣ ਜੋ ਦਿਖਾਉਂਦਾ ਹੈ ਕਿ ਏਆਈ ਸੁਰੱਖਿਆ ਫਿਲਟਰ ਕਿਵੇਂ ਕੰਮ ਕਰਦੇ ਹਨ
- **ਸਭ ਤੋਂ ਵਧੀਆ ਤਰੀਕੇ**: ਨੈਤਿਕ ਏਆਈ ਵਿਕਾਸ ਅਤੇ ਤੈਨਾਤੀ ਲਈ ਜ਼ਰੂਰੀ ਦਿਸ਼ਾ-ਨਿਰਦੇਸ਼
- **[→ ਅਧਿਆਇ 5 ਸ਼ੁਰੂ ਕਰੋ](./05-ResponsibleGenAI/README.md)**

## ਵਾਧੂ ਸਰੋਤ

- [ਸ਼ੁਰੂਆਤੀਆਂ ਲਈ ਏਆਈ ਏਜੰਟ](https://github.com/microsoft/ai-agents-for-beginners)
- [ਸ਼ੁਰੂਆਤੀਆਂ ਲਈ ਜਨਰੇਟਿਵ ਏਆਈ .NET ਵਰਤੋਂ](https://github.com/microsoft/Generative-AI-for-beginners-dotnet)
- [ਸ਼ੁਰੂਆਤੀਆਂ ਲਈ ਜਨਰੇਟਿਵ ਏਆਈ ਜਾਵਾਸਕ੍ਰਿਪਟ ਵਰਤੋਂ](https://github.com/microsoft/generative-ai-with-javascript)
- [ਸ਼ੁਰੂਆਤੀਆਂ ਲਈ ਜਨਰੇਟਿਵ ਏਆਈ](https://github.com/microsoft/generative-ai-for-beginners)
- [ਸ਼ੁਰੂਆਤੀਆਂ ਲਈ ਮਸ਼ੀਨ ਲਰਨਿੰਗ](https://aka.ms/ml-beginners)
- [ਸ਼ੁਰੂਆਤੀਆਂ ਲਈ ਡਾਟਾ ਸਾਇੰਸ](https://aka.ms/datascience-beginners)
- [ਸ਼ੁਰੂਆਤੀਆਂ ਲਈ ਏਆਈ](https://aka.ms/ai-beginners)
- [ਸ਼ੁਰੂਆਤੀਆਂ ਲਈ ਸਾਈਬਰਸੁਰੱਖਿਆ](https://github.com/microsoft/Security-101)
- [ਸ਼ੁਰੂਆਤੀਆਂ ਲਈ ਵੈੱਬ ਡਿਵੈਲਪਮੈਂਟ](https://aka.ms/webdev-beginners)
- [ਸ਼ੁਰੂਆਤੀਆਂ ਲਈ IoT](https://aka.ms/iot-beginners)
- [ਸ਼ੁਰੂਆਤੀਆਂ ਲਈ XR ਵਿਕਾਸ](https://github.com/microsoft/xr-development-for-beginners)
- [GitHub Copilot ਲਈ ਮਾਹਰ ਬਣੋ - ਏਆਈ ਜੋੜੇ ਹੋਏ ਪ੍ਰੋਗਰਾਮਿੰਗ ਲਈ](https://aka.ms/GitHubCopilotAI)
- [C#/.NET ਡਿਵੈਲਪਰਾਂ ਲਈ GitHub Copilot ਵਿੱਚ ਮਾਹਰ ਬਣੋ](https://github.com/microsoft/mastering-github-copilot-for-dotnet-csharp-developers)
- [ਆਪਣੇ Copilot ਸਫਰ ਦੀ ਚੋਣ ਕਰੋ](https://github.com/microsoft/CopilotAdventures)
- [RAG ਚੈਟ ਐਪ Azure AI ਸੇਵਾਵਾਂ ਨਾਲ](https://github.com/Azure-Samples/azure-search-openai-demo-java)

**ਅਸਵੀਕਰਤਾ**:  
ਇਹ ਦਸਤਾਵੇਜ਼ AI ਅਨੁਵਾਦ ਸੇਵਾ [Co-op Translator](https://github.com/Azure/co-op-translator) ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਅਨੁਵਾਦ ਕੀਤਾ ਗਿਆ ਹੈ। ਹਾਲਾਂਕਿ ਅਸੀਂ ਸਹੀਅਤ ਲਈ ਯਤਨਸ਼ੀਲ ਹਾਂ, ਕਿਰਪਾ ਕਰਕੇ ਧਿਆਨ ਦਿਓ ਕਿ ਸਵੈਚਾਲਿਤ ਅਨੁਵਾਦਾਂ ਵਿੱਚ ਗਲਤੀਆਂ ਜਾਂ ਅਸੁਚਨਾਵਾਂ ਹੋ ਸਕਦੀਆਂ ਹਨ। ਮੂਲ ਦਸਤਾਵੇਜ਼ ਨੂੰ ਇਸਦੀ ਮੂਲ ਭਾਸ਼ਾ ਵਿੱਚ ਅਧਿਕਾਰਤ ਸਰੋਤ ਮੰਨਿਆ ਜਾਣਾ ਚਾਹੀਦਾ ਹੈ। ਮਹੱਤਵਪੂਰਨ ਜਾਣਕਾਰੀ ਲਈ, ਪੇਸ਼ੇਵਰ ਮਨੁੱਖੀ ਅਨੁਵਾਦ ਦੀ ਸਿਫਾਰਸ਼ ਕੀਤੀ ਜਾਂਦੀ ਹੈ। ਇਸ ਅਨੁਵਾਦ ਦੀ ਵਰਤੋਂ ਤੋਂ ਪੈਦਾ ਹੋਣ ਵਾਲੇ ਕਿਸੇ ਵੀ ਗਲਤਫਹਿਮੀ ਜਾਂ ਗਲਤ ਵਿਆਖਿਆ ਲਈ ਅਸੀਂ ਜ਼ਿੰਮੇਵਾਰ ਨਹੀਂ ਹਾਂ।