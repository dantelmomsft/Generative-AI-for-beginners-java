<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "59454ab4ec36d89840df6fcfe7633cbd",
  "translation_date": "2025-07-25T11:53:52+00:00",
  "source_file": "03-CoreGenerativeAITechniques/README.md",
  "language_code": "sk"
}
-->
# Návod na základné techniky generatívnej AI

## Obsah

- [Predpoklady](../../../03-CoreGenerativeAITechniques)
- [Začíname](../../../03-CoreGenerativeAITechniques)
  - [Krok 1: Nastavte svoju environmentálnu premennú](../../../03-CoreGenerativeAITechniques)
  - [Krok 2: Prejdite do adresára s príkladmi](../../../03-CoreGenerativeAITechniques)
- [Návod 1: LLM dopĺňanie a chat](../../../03-CoreGenerativeAITechniques)
- [Návod 2: Volanie funkcií](../../../03-CoreGenerativeAITechniques)
- [Návod 3: RAG (Generovanie s podporou vyhľadávania)](../../../03-CoreGenerativeAITechniques)
- [Návod 4: Zodpovedná AI](../../../03-CoreGenerativeAITechniques)
- [Spoločné vzory v príkladoch](../../../03-CoreGenerativeAITechniques)
- [Ďalšie kroky](../../../03-CoreGenerativeAITechniques)
- [Riešenie problémov](../../../03-CoreGenerativeAITechniques)
  - [Bežné problémy](../../../03-CoreGenerativeAITechniques)

## Prehľad

Tento návod poskytuje praktické príklady základných techník generatívnej AI pomocou Javy a GitHub Models. Naučíte sa, ako pracovať s veľkými jazykovými modelmi (LLMs), implementovať volanie funkcií, používať generovanie s podporou vyhľadávania (RAG) a aplikovať zásady zodpovednej AI.

## Predpoklady

Pred začiatkom sa uistite, že máte:
- Nainštalovanú Javu 21 alebo vyššiu
- Maven na správu závislostí
- GitHub účet s osobným prístupovým tokenom (PAT)

## Začíname

### Krok 1: Nastavte svoju environmentálnu premennú

Najprv musíte nastaviť svoj GitHub token ako environmentálnu premennú. Tento token vám umožní bezplatný prístup k GitHub Models.

**Windows (Command Prompt):**
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

### Krok 2: Prejdite do adresára s príkladmi

```bash
cd 03-CoreGenerativeAITechniques/examples/
```

## Návod 1: LLM dopĺňanie a chat

**Súbor:** `src/main/java/com/example/genai/techniques/completions/LLMCompletionsApp.java`

### Čo vás tento príklad naučí

Tento príklad demonštruje základné mechanizmy interakcie s veľkými jazykovými modelmi (LLM) prostredníctvom OpenAI API, vrátane inicializácie klienta s GitHub Models, vzorov štruktúry správ pre systémové a používateľské výzvy, správy stavu konverzácie prostredníctvom akumulácie histórie správ a ladenia parametrov na kontrolu dĺžky odpovede a úrovne kreativity.

### Kľúčové koncepty kódu

#### 1. Nastavenie klienta
```java
// Create the AI client
OpenAIClient client = new OpenAIClientBuilder()
    .endpoint("https://models.inference.ai.azure.com")
    .credential(new StaticTokenCredential(pat))
    .buildClient();
```

Toto vytvorí spojenie s GitHub Models pomocou vášho tokenu.

#### 2. Jednoduché dopĺňanie
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

#### 3. Pamäť konverzácie
```java
// Add AI's response to maintain conversation history
messages.add(new ChatRequestAssistantMessage(aiResponse));
messages.add(new ChatRequestUserMessage("Follow-up question"));
```

AI si pamätá predchádzajúce správy iba vtedy, ak ich zahrniete do nasledujúcich požiadaviek.

### Spustenie príkladu
```bash
mvn compile exec:java -Dexec.mainClass="com.example.genai.techniques.completions.LLMCompletionsApp"
```

### Čo sa stane, keď ho spustíte

1. **Jednoduché dopĺňanie**: AI odpovie na otázku o Jave s pomocou systémovej výzvy
2. **Viackolový chat**: AI si udržiava kontext naprieč viacerými otázkami
3. **Interaktívny chat**: Môžete viesť skutočnú konverzáciu s AI

## Návod 2: Volanie funkcií

**Súbor:** `src/main/java/com/example/genai/techniques/functions/FunctionsApp.java`

### Čo vás tento príklad naučí

Volanie funkcií umožňuje modelom AI požadovať vykonanie externých nástrojov a API prostredníctvom štruktúrovaného protokolu, kde model analyzuje požiadavky v prirodzenom jazyku, určuje potrebné volania funkcií s vhodnými parametrami pomocou definícií JSON Schema a spracováva vrátené výsledky na generovanie kontextových odpovedí, pričom samotné vykonanie funkcií zostáva pod kontrolou vývojára kvôli bezpečnosti a spoľahlivosti.

### Kľúčové koncepty kódu

#### 1. Definícia funkcie
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

Toto informuje AI, aké funkcie sú dostupné a ako ich používať.

#### 2. Tok vykonania funkcie
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

#### 3. Implementácia funkcie
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

### Spustenie príkladu
```bash
mvn compile exec:java -Dexec.mainClass="com.example.genai.techniques.functions.FunctionsApp"
```

### Čo sa stane, keď ho spustíte

1. **Funkcia počasia**: AI požaduje údaje o počasí v Seattli, vy ich poskytnete, AI formátuje odpoveď
2. **Funkcia kalkulačky**: AI požaduje výpočet (15 % z 240), vy ho vykonáte, AI vysvetlí výsledok

## Návod 3: RAG (Generovanie s podporou vyhľadávania)

**Súbor:** `src/main/java/com/example/genai/techniques/rag/SimpleReaderDemo.java`

### Čo vás tento príklad naučí

Generovanie s podporou vyhľadávania (RAG) kombinuje vyhľadávanie informácií s generovaním textu tým, že vkladá kontext externých dokumentov do výziev AI, čo umožňuje modelom poskytovať presné odpovede na základe konkrétnych zdrojov poznatkov namiesto potenciálne zastaraných alebo nepresných tréningových údajov, pričom si zachováva jasné hranice medzi otázkami používateľa a autoritatívnymi zdrojmi informácií prostredníctvom strategického návrhu výziev.

### Kľúčové koncepty kódu

#### 1. Načítanie dokumentu
```java
// Load your knowledge source
String doc = Files.readString(Paths.get("document.txt"));
```

#### 2. Vkladanie kontextu
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

Trojnité úvodzovky pomáhajú AI rozlíšiť medzi kontextom a otázkou.

#### 3. Bezpečné spracovanie odpovedí
```java
if (response != null && response.getChoices() != null && !response.getChoices().isEmpty()) {
    String answer = response.getChoices().get(0).getMessage().getContent();
    System.out.println("Assistant: " + answer);
} else {
    System.err.println("Error: No response received from the API.");
}
```

Vždy validujte odpovede API, aby ste predišli zlyhaniam.

### Spustenie príkladu
```bash
mvn compile exec:java -Dexec.mainClass="com.example.genai.techniques.rag.SimpleReaderDemo"
```

### Čo sa stane, keď ho spustíte

1. Program načíta `document.txt` (obsahuje informácie o GitHub Models)
2. Položíte otázku o dokumente
3. AI odpovie iba na základe obsahu dokumentu, nie na základe svojich všeobecných znalostí

Skúste sa opýtať: "Čo sú GitHub Models?" vs "Aké je počasie?"

## Návod 4: Zodpovedná AI

**Súbor:** `src/main/java/com/example/genai/techniques/responsibleai/ResponsibleGithubModels.java`

### Čo vás tento príklad naučí

Príklad Zodpovednej AI ukazuje dôležitosť implementácie bezpečnostných opatrení v AI aplikáciách. Demonštruje bezpečnostné filtre, ktoré detekujú škodlivé kategórie obsahu vrátane nenávistných prejavov, obťažovania, sebapoškodzovania, sexuálneho obsahu a násilia, pričom ukazuje, ako by produkčné AI aplikácie mali elegantne riešiť porušenia politík obsahu prostredníctvom správneho spracovania výnimiek, mechanizmov spätnej väzby používateľov a stratégií náhradných odpovedí.

### Kľúčové koncepty kódu

#### 1. Rámec testovania bezpečnosti
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

#### 2. Testované kategórie bezpečnosti
- Pokyny na násilie/poškodenie
- Nenávistné prejavy
- Porušenie súkromia
- Lekárske dezinformácie
- Nelegálne aktivity

### Spustenie príkladu
```bash
mvn compile exec:java -Dexec.mainClass="com.example.genai.techniques.responsibleai.ResponsibleGithubModels"
```

### Čo sa stane, keď ho spustíte

Program testuje rôzne škodlivé výzvy a ukazuje, ako systém AI bezpečnosti:
1. **Blokuje nebezpečné požiadavky** pomocou HTTP 400 chýb
2. **Povoľuje bezpečný obsah** na generovanie
3. **Chráni používateľov** pred škodlivými výstupmi AI

## Spoločné vzory v príkladoch

### Vzor autentifikácie
Všetky príklady používajú tento vzor na autentifikáciu s GitHub Models:

```java
String pat = System.getenv("GITHUB_TOKEN");
TokenCredential credential = new StaticTokenCredential(pat);
OpenAIClient client = new OpenAIClientBuilder()
    .endpoint("https://models.inference.ai.azure.com")
    .credential(credential)
    .buildClient();
```

### Vzor spracovania chýb
```java
try {
    // AI operation
} catch (HttpResponseException e) {
    // Handle API errors (rate limits, safety filters)
} catch (Exception e) {
    // Handle general errors (network, parsing)
}
```

### Vzor štruktúry správ
```java
List<ChatRequestMessage> messages = List.of(
    new ChatRequestSystemMessage("Set AI behavior"),
    new ChatRequestUserMessage("User's actual request")
);
```

## Ďalšie kroky

[Kap. 04: Praktické príklady](../04-PracticalSamples/README.md)

## Riešenie problémov

### Bežné problémy

**"GITHUB_TOKEN nie je nastavený"**
- Uistite sa, že ste nastavili environmentálnu premennú
- Overte, že váš token má rozsah `models:read`

**"Žiadna odpoveď od API"**
- Skontrolujte svoje internetové pripojenie
- Overte, že váš token je platný
- Skontrolujte, či ste neprekročili limity požiadaviek

**Chyby kompilácie Maven**
- Uistite sa, že máte Javu 21 alebo vyššiu
- Spustite `mvn clean compile`, aby ste obnovili závislosti

**Zrieknutie sa zodpovednosti**:  
Tento dokument bol preložený pomocou služby AI prekladu [Co-op Translator](https://github.com/Azure/co-op-translator). Aj keď sa snažíme o presnosť, prosím, berte na vedomie, že automatizované preklady môžu obsahovať chyby alebo nepresnosti. Pôvodný dokument v jeho rodnom jazyku by mal byť považovaný za autoritatívny zdroj. Pre kritické informácie sa odporúča profesionálny ľudský preklad. Nezodpovedáme za žiadne nedorozumenia alebo nesprávne interpretácie vyplývajúce z použitia tohto prekladu.