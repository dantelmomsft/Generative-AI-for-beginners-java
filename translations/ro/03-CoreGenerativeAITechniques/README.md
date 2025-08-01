<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "59454ab4ec36d89840df6fcfe7633cbd",
  "translation_date": "2025-07-25T11:56:01+00:00",
  "source_file": "03-CoreGenerativeAITechniques/README.md",
  "language_code": "ro"
}
-->
# Tutorial Tehnici de Bază AI Generativ

## Cuprins

- [Prerechizite](../../../03-CoreGenerativeAITechniques)
- [Începeți](../../../03-CoreGenerativeAITechniques)
  - [Pasul 1: Setarea Variabilei de Mediu](../../../03-CoreGenerativeAITechniques)
  - [Pasul 2: Navigați la Directorul de Exemple](../../../03-CoreGenerativeAITechniques)
- [Tutorial 1: Completări și Chat LLM](../../../03-CoreGenerativeAITechniques)
- [Tutorial 2: Apelarea Funcțiilor](../../../03-CoreGenerativeAITechniques)
- [Tutorial 3: RAG (Generare Augmentată prin Recuperare)](../../../03-CoreGenerativeAITechniques)
- [Tutorial 4: AI Responsabil](../../../03-CoreGenerativeAITechniques)
- [Tipare Comune în Exemple](../../../03-CoreGenerativeAITechniques)
- [Pași Următori](../../../03-CoreGenerativeAITechniques)
- [Depanare](../../../03-CoreGenerativeAITechniques)
  - [Probleme Comune](../../../03-CoreGenerativeAITechniques)

## Prezentare Generală

Acest tutorial oferă exemple practice ale tehnicilor de bază AI generativ utilizând Java și Modelele GitHub. Veți învăța cum să interacționați cu Modele de Limbaj Extins (LLMs), să implementați apelarea funcțiilor, să utilizați generarea augmentată prin recuperare (RAG) și să aplicați practici de AI responsabil.

## Prerechizite

Înainte de a începe, asigurați-vă că aveți:
- Java 21 sau o versiune mai recentă instalată
- Maven pentru gestionarea dependențelor
- Un cont GitHub cu un token de acces personal (PAT)

## Începeți

### Pasul 1: Setarea Variabilei de Mediu

Mai întâi, trebuie să setați token-ul GitHub ca variabilă de mediu. Acest token vă permite să accesați Modelele GitHub gratuit.

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

### Pasul 2: Navigați la Directorul de Exemple

```bash
cd 03-CoreGenerativeAITechniques/examples/
```

## Tutorial 1: Completări și Chat LLM

**Fișier:** `src/main/java/com/example/genai/techniques/completions/LLMCompletionsApp.java`

### Ce Învață Acest Exemplu

Acest exemplu demonstrează mecanismele de bază ale interacțiunii cu Modelele de Limbaj Extins (LLM) prin API-ul OpenAI, inclusiv inițializarea clientului cu Modelele GitHub, tipare de structură a mesajelor pentru prompturi de sistem și utilizator, gestionarea stării conversației prin acumularea istoricului mesajelor și ajustarea parametrilor pentru controlul lungimii răspunsurilor și nivelurilor de creativitate.

### Concepte Cheie ale Codului

#### 1. Configurarea Clientului
```java
// Create the AI client
OpenAIClient client = new OpenAIClientBuilder()
    .endpoint("https://models.inference.ai.azure.com")
    .credential(new StaticTokenCredential(pat))
    .buildClient();
```

Aceasta creează o conexiune la Modelele GitHub utilizând token-ul dvs.

#### 2. Completare Simplă
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

#### 3. Memoria Conversației
```java
// Add AI's response to maintain conversation history
messages.add(new ChatRequestAssistantMessage(aiResponse));
messages.add(new ChatRequestUserMessage("Follow-up question"));
```

AI își amintește mesajele anterioare doar dacă le includeți în cererile ulterioare.

### Rulați Exemplul
```bash
mvn compile exec:java -Dexec.mainClass="com.example.genai.techniques.completions.LLMCompletionsApp"
```

### Ce Se Întâmplă Când Îl Rulați

1. **Completare Simplă**: AI răspunde la o întrebare despre Java cu ghidaj din promptul de sistem
2. **Chat Multi-turn**: AI menține contextul pe parcursul mai multor întrebări
3. **Chat Interactiv**: Puteți avea o conversație reală cu AI

## Tutorial 2: Apelarea Funcțiilor

**Fișier:** `src/main/java/com/example/genai/techniques/functions/FunctionsApp.java`

### Ce Învață Acest Exemplu

Apelarea funcțiilor permite modelelor AI să solicite executarea unor instrumente și API-uri externe printr-un protocol structurat, unde modelul analizează cererile în limbaj natural, determină apelurile de funcții necesare cu parametrii corespunzători utilizând definiții JSON Schema și procesează rezultatele returnate pentru a genera răspunsuri contextuale, în timp ce execuția efectivă a funcțiilor rămâne sub controlul dezvoltatorului pentru securitate și fiabilitate.

### Concepte Cheie ale Codului

#### 1. Definirea Funcției
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

Aceasta spune AI ce funcții sunt disponibile și cum să le utilizeze.

#### 2. Fluxul de Execuție al Funcției
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

#### 3. Implementarea Funcției
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

### Rulați Exemplul
```bash
mvn compile exec:java -Dexec.mainClass="com.example.genai.techniques.functions.FunctionsApp"
```

### Ce Se Întâmplă Când Îl Rulați

1. **Funcția Meteo**: AI solicită date meteo pentru Seattle, dvs. le furnizați, AI formatează un răspuns
2. **Funcția Calculator**: AI solicită un calcul (15% din 240), dvs. îl efectuați, AI explică rezultatul

## Tutorial 3: RAG (Generare Augmentată prin Recuperare)

**Fișier:** `src/main/java/com/example/genai/techniques/rag/SimpleReaderDemo.java`

### Ce Învață Acest Exemplu

Generarea Augmentată prin Recuperare (RAG) combină recuperarea informațiilor cu generarea de limbaj prin injectarea contextului documentelor externe în prompturile AI, permițând modelelor să ofere răspunsuri precise bazate pe surse de cunoștințe specifice, mai degrabă decât pe date de antrenament potențial depășite sau inexacte, menținând în același timp limite clare între întrebările utilizatorului și sursele de informații autoritative prin inginerie strategică a prompturilor.

### Concepte Cheie ale Codului

#### 1. Încărcarea Documentului
```java
// Load your knowledge source
String doc = Files.readString(Paths.get("document.txt"));
```

#### 2. Injectarea Contextului
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

Triplele ghilimele ajută AI să distingă între context și întrebare.

#### 3. Gestionarea Sigură a Răspunsurilor
```java
if (response != null && response.getChoices() != null && !response.getChoices().isEmpty()) {
    String answer = response.getChoices().get(0).getMessage().getContent();
    System.out.println("Assistant: " + answer);
} else {
    System.err.println("Error: No response received from the API.");
}
```

Validați întotdeauna răspunsurile API pentru a preveni blocările.

### Rulați Exemplul
```bash
mvn compile exec:java -Dexec.mainClass="com.example.genai.techniques.rag.SimpleReaderDemo"
```

### Ce Se Întâmplă Când Îl Rulați

1. Programul încarcă `document.txt` (conține informații despre Modelele GitHub)
2. Puneți o întrebare despre document
3. AI răspunde bazându-se doar pe conținutul documentului, nu pe cunoștințele sale generale

Încercați să întrebați: "Ce sunt Modelele GitHub?" vs "Cum este vremea?"

## Tutorial 4: AI Responsabil

**Fișier:** `src/main/java/com/example/genai/techniques/responsibleai/ResponsibleGithubModels.java`

### Ce Învață Acest Exemplu

Exemplul AI Responsabil evidențiază importanța implementării măsurilor de siguranță în aplicațiile AI. Demonstrează filtre de siguranță care detectează categorii de conținut dăunător, inclusiv discurs de ură, hărțuire, auto-vătămare, conținut sexual și violență, arătând cum aplicațiile AI de producție ar trebui să gestioneze cu grație încălcările politicii de conținut prin gestionarea corespunzătoare a excepțiilor, mecanisme de feedback pentru utilizatori și strategii de răspuns alternativ.

### Concepte Cheie ale Codului

#### 1. Cadru de Testare a Siguranței
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

#### 2. Categorii de Siguranță Testate
- Instrucțiuni de violență/vătămare
- Discurs de ură
- Încălcări ale confidențialității
- Dezinformare medicală
- Activități ilegale

### Rulați Exemplul
```bash
mvn compile exec:java -Dexec.mainClass="com.example.genai.techniques.responsibleai.ResponsibleGithubModels"
```

### Ce Se Întâmplă Când Îl Rulați

Programul testează diverse prompturi dăunătoare și arată cum sistemul de siguranță AI:
1. **Blochează cererile periculoase** cu erori HTTP 400
2. **Permite generarea conținutului sigur** în mod normal
3. **Protejează utilizatorii** de ieșirile dăunătoare ale AI

## Tipare Comune în Exemple

### Tipar de Autentificare
Toate exemplele utilizează acest tipar pentru autentificarea cu Modelele GitHub:

```java
String pat = System.getenv("GITHUB_TOKEN");
TokenCredential credential = new StaticTokenCredential(pat);
OpenAIClient client = new OpenAIClientBuilder()
    .endpoint("https://models.inference.ai.azure.com")
    .credential(credential)
    .buildClient();
```

### Tipar de Gestionare a Erorilor
```java
try {
    // AI operation
} catch (HttpResponseException e) {
    // Handle API errors (rate limits, safety filters)
} catch (Exception e) {
    // Handle general errors (network, parsing)
}
```

### Tipar de Structură a Mesajelor
```java
List<ChatRequestMessage> messages = List.of(
    new ChatRequestSystemMessage("Set AI behavior"),
    new ChatRequestUserMessage("User's actual request")
);
```

## Pași Următori

[Capitolul 04: Exemple practice](../04-PracticalSamples/README.md)

## Depanare

### Probleme Comune

**"GITHUB_TOKEN not set"**
- Asigurați-vă că ați setat variabila de mediu
- Verificați dacă token-ul dvs. are scopul `models:read`

**"No response from API"**
- Verificați conexiunea la internet
- Verificați dacă token-ul dvs. este valid
- Verificați dacă ați atins limitele de rată

**Erori de compilare Maven**
- Asigurați-vă că aveți Java 21 sau o versiune mai recentă
- Rulați `mvn clean compile` pentru a reîmprospăta dependențele

**Declinare de responsabilitate**:  
Acest document a fost tradus folosind serviciul de traducere AI [Co-op Translator](https://github.com/Azure/co-op-translator). Deși ne străduim să asigurăm acuratețea, vă rugăm să fiți conștienți că traducerile automate pot conține erori sau inexactități. Documentul original în limba sa natală ar trebui considerat sursa autoritară. Pentru informații critice, se recomandă traducerea profesională realizată de un specialist uman. Nu ne asumăm responsabilitatea pentru eventualele neînțelegeri sau interpretări greșite care pot apărea din utilizarea acestei traduceri.