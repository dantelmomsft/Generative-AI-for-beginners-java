<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "40abf4889418bff189039ac30ff44281",
  "translation_date": "2025-07-23T12:14:48+00:00",
  "source_file": "02-SetupDevEnvironment/README.md",
  "language_code": "it"
}
-->
# Configurare l'Ambiente di Sviluppo per Generative AI con Java

> **Avvio Rapido**: Codifica nel Cloud in 2 minuti - Vai a [Configurazione GitHub Codespaces](../../../02-SetupDevEnvironment) - nessuna installazione locale richiesta e utilizza i modelli di GitHub!

> **Interessato ad Azure OpenAI?**, consulta la nostra [Guida alla Configurazione di Azure OpenAI](getting-started-azure-openai.md) con i passaggi per creare una nuova risorsa Azure OpenAI.

## Cosa Imparerai

- Configurare un ambiente di sviluppo Java per applicazioni AI
- Scegliere e configurare il tuo ambiente di sviluppo preferito (cloud-first con Codespaces, container locale, o configurazione locale completa)
- Testare la configurazione collegandoti ai modelli di GitHub

## Indice

- [Cosa Imparerai](../../../02-SetupDevEnvironment)
- [Introduzione](../../../02-SetupDevEnvironment)
- [Passo 1: Configura il tuo Ambiente di Sviluppo](../../../02-SetupDevEnvironment)
  - [Opzione A: GitHub Codespaces (Consigliato)](../../../02-SetupDevEnvironment)
  - [Opzione B: Container Locale](../../../02-SetupDevEnvironment)
  - [Opzione C: Usa la tua Installazione Locale Esistente](../../../02-SetupDevEnvironment)
- [Passo 2: Crea un Token di Accesso Personale GitHub](../../../02-SetupDevEnvironment)
- [Passo 3: Testa la Configurazione](../../../02-SetupDevEnvironment)
- [Risoluzione dei Problemi](../../../02-SetupDevEnvironment)
- [Riepilogo](../../../02-SetupDevEnvironment)
- [Prossimi Passi](../../../02-SetupDevEnvironment)

## Introduzione

Questo capitolo ti guiderà nella configurazione di un ambiente di sviluppo. Utilizzeremo **GitHub Models** come esempio principale perché è gratuito, facile da configurare con un account GitHub, non richiede una carta di credito e offre accesso a diversi modelli per sperimentare.

**Nessuna configurazione locale richiesta!** Puoi iniziare a codificare immediatamente utilizzando GitHub Codespaces, che fornisce un ambiente di sviluppo completo direttamente nel tuo browser.

<img src="./images/models.webp" alt="Screenshot: GitHub Models" width="50%">

Consigliamo di utilizzare [**GitHub Models**](https://github.com/marketplace?type=models) per questo corso perché:
- È **gratuito** per iniziare
- È **facile** da configurare con un account GitHub
- **Non richiede carta di credito**
- Offre **modelli multipli** per sperimentare

> **Nota**: I modelli di GitHub utilizzati in questa formazione hanno i seguenti limiti gratuiti:
> - 15 richieste al minuto (150 al giorno)
> - ~8.000 parole in ingresso, ~4.000 parole in uscita per richiesta
> - 5 richieste simultanee
> 
> Per uso in produzione, aggiorna ai modelli Azure AI Foundry con il tuo account Azure. Il tuo codice non necessita di modifiche. Consulta la [documentazione di Azure AI Foundry](https://learn.microsoft.com/azure/ai-foundry/foundry-models/how-to/quickstart-github-models).

## Passo 1: Configura il tuo Ambiente di Sviluppo

<a name="quick-start-cloud"></a>

Abbiamo creato un container di sviluppo preconfigurato per ridurre al minimo il tempo di configurazione e garantire che tu abbia tutti gli strumenti necessari per questo corso su Generative AI con Java. Scegli il tuo approccio di sviluppo preferito:

### Opzioni di Configurazione dell'Ambiente:

#### Opzione A: GitHub Codespaces (Consigliato)

**Inizia a codificare in 2 minuti - nessuna configurazione locale richiesta!**

1. Fai un fork di questo repository nel tuo account GitHub
   > **Nota**: Se desideri modificare la configurazione di base, consulta la [Configurazione del Container di Sviluppo](../../../.devcontainer/devcontainer.json)
2. Clicca su **Code** → scheda **Codespaces** → **...** → **New with options...**
3. Usa le impostazioni predefinite – questo selezionerà la **Configurazione del container di sviluppo**: **Generative AI Java Development Environment** creato appositamente per questo corso
4. Clicca su **Create codespace**
5. Attendi ~2 minuti affinché l'ambiente sia pronto
6. Procedi al [Passo 2: Crea Token GitHub](../../../02-SetupDevEnvironment)

<img src="./images/codespaces.png" alt="Screenshot: Sottomenu Codespaces" width="50%">

<img src="./images/image.png" alt="Screenshot: Nuovo con opzioni" width="50%">

<img src="./images/codespaces-create.png" alt="Screenshot: Opzioni per creare codespace" width="50%">

> **Vantaggi di Codespaces**:
> - Nessuna installazione locale richiesta
> - Funziona su qualsiasi dispositivo con un browser
> - Preconfigurato con tutti gli strumenti e le dipendenze
> - 60 ore gratuite al mese per account personali
> - Ambiente coerente per tutti i partecipanti

#### Opzione B: Container Locale

**Per sviluppatori che preferiscono lo sviluppo locale con Docker**

1. Fai un fork e clona questo repository sulla tua macchina locale
   > **Nota**: Se desideri modificare la configurazione di base, consulta la [Configurazione del Container di Sviluppo](../../../.devcontainer/devcontainer.json)
2. Installa [Docker Desktop](https://www.docker.com/products/docker-desktop/) e [VS Code](https://code.visualstudio.com/)
3. Installa l'[estensione Dev Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) in VS Code
4. Apri la cartella del repository in VS Code
5. Quando richiesto, clicca su **Reopen in Container** (o usa `Ctrl+Shift+P` → "Dev Containers: Reopen in Container")
6. Attendi che il container venga costruito e avviato
7. Procedi al [Passo 2: Crea Token GitHub](../../../02-SetupDevEnvironment)

<img src="./images/devcontainer.png" alt="Screenshot: Configurazione del container di sviluppo" width="50%">

<img src="./images/image-3.png" alt="Screenshot: Costruzione del container completata" width="50%">

#### Opzione C: Usa la tua Installazione Locale Esistente

**Per sviluppatori con ambienti Java già configurati**

Prerequisiti:
- [Java 21+](https://www.oracle.com/java/technologies/javase/jdk21-archive-downloads.html) 
- [Maven 3.9+](https://maven.apache.org/download.cgi)
- [VS Code](https://code.visualstudio.com) o il tuo IDE preferito

Passaggi:
1. Clona questo repository sulla tua macchina locale
2. Apri il progetto nel tuo IDE
3. Procedi al [Passo 2: Crea Token GitHub](../../../02-SetupDevEnvironment)

> **Suggerimento Pro**: Se hai una macchina con specifiche basse ma vuoi usare VS Code localmente, utilizza GitHub Codespaces! Puoi collegare il tuo VS Code locale a un Codespace ospitato nel cloud per ottenere il meglio di entrambi i mondi.

<img src="./images/image-2.png" alt="Screenshot: Istanza locale del container di sviluppo creata" width="50%">

## Passo 2: Crea un Token di Accesso Personale GitHub

1. Vai su [Impostazioni GitHub](https://github.com/settings/profile) e seleziona **Settings** dal menu del tuo profilo.
2. Nella barra laterale sinistra, clicca su **Developer settings** (di solito in fondo).
3. Sotto **Personal access tokens**, clicca su **Fine-grained tokens** (o segui questo [link diretto](https://github.com/settings/personal-access-tokens)).
4. Clicca su **Generate new token**.
5. Sotto "Token name", fornisci un nome descrittivo (es. `GenAI-Java-Course-Token`).
6. Imposta una data di scadenza (consigliato: 7 giorni per migliori pratiche di sicurezza).
7. Sotto "Resource owner", seleziona il tuo account utente.
8. Sotto "Repository access", seleziona i repository che vuoi usare con GitHub Models (o "All repositories" se necessario).
9. Sotto "Repository permissions", trova **Models** e impostalo su **Read and write**.
10. Clicca su **Generate token**.
11. **Copia e salva il tuo token ora** – non lo vedrai più!

> **Consiglio di Sicurezza**: Usa il minimo ambito richiesto e il tempo di scadenza più breve possibile per i tuoi token di accesso.

## Passo 3: Testa la Configurazione con l'Esempio GitHub Models

Una volta che il tuo ambiente di sviluppo è pronto, testiamo l'integrazione con GitHub Models utilizzando la nostra applicazione di esempio in [`02-SetupDevEnvironment/src/github-models`](../../../02-SetupDevEnvironment/src/github-models).

1. Apri il terminale nel tuo ambiente di sviluppo.
2. Vai all'esempio GitHub Models:
   ```bash
   cd 02-SetupDevEnvironment/src/github-models
   ```
3. Imposta il tuo token GitHub come variabile d'ambiente:
   ```bash
   # macOS/Linux
   export GITHUB_TOKEN=your_token_here
   
   # Windows (Command Prompt)
   set GITHUB_TOKEN=your_token_here
   
   # Windows (PowerShell)
   $env:GITHUB_TOKEN="your_token_here"
   ```

4. Esegui l'applicazione:
   ```bash
   mvn compile exec:java -Dexec.mainClass="com.example.githubmodels.App"
   ```

Dovresti vedere un output simile a:
```text
Using model: gpt-4.1-nano
Sending request to GitHub Models...
Response: Hello World!
```

### Comprendere il Codice di Esempio

Prima, capiamo cosa abbiamo appena eseguito. L'esempio sotto `src/github-models` utilizza l'SDK Java di OpenAI per connettersi ai modelli di GitHub:

**Cosa fa questo codice:**
- **Si connette** ai modelli di GitHub utilizzando il tuo token di accesso personale
- **Invia** un semplice messaggio "Say Hello World!" al modello AI
- **Riceve** e visualizza la risposta dell'AI
- **Valida** che la configurazione funzioni correttamente

**Dipendenza Chiave** (in `pom.xml`):
```xml
<dependency>
    <groupId>com.openai</groupId>
    <artifactId>openai-java</artifactId>
    <version>2.12.0</version>
</dependency>
```

**Codice Principale** (`App.java`):
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

## Riepilogo

**Congratulazioni!** Hai completato con successo:

- **Creazione di un Token di Accesso Personale GitHub** con permessi adeguati per l'accesso ai modelli AI
- **Configurazione del tuo ambiente di sviluppo Java** utilizzando Codespaces, container di sviluppo o installazione locale
- **Connessione ai modelli di GitHub** utilizzando l'SDK Java di OpenAI per l'accesso gratuito allo sviluppo AI
- **Test dell'integrazione** con un'applicazione di esempio funzionante che comunica con i modelli AI

## Prossimi Passi

[Capitolo 3: Tecniche Core di Generative AI](../03-CoreGenerativeAITechniques/README.md)

## Risoluzione dei Problemi

Hai problemi? Ecco problemi comuni e soluzioni:

- **Token non funzionante?** 
  - Assicurati di aver copiato l'intero token senza spazi extra
  - Verifica che il token sia impostato correttamente come variabile d'ambiente
  - Controlla che il tuo token abbia i permessi corretti (Models: Read and write)

- **Maven non trovato?** 
  - Se usi container di sviluppo/Codespaces, Maven dovrebbe essere preinstallato
  - Per configurazioni locali, assicurati che Java 21+ e Maven 3.9+ siano installati
  - Prova `mvn --version` per verificare l'installazione

- **Problemi di connessione?** 
  - Controlla la tua connessione internet
  - Verifica che GitHub sia accessibile dalla tua rete
  - Assicurati di non essere dietro un firewall che blocca l'endpoint dei modelli di GitHub

- **Container di sviluppo non avviato?** 
  - Assicurati che Docker Desktop sia in esecuzione (per sviluppo locale)
  - Prova a ricostruire il container: `Ctrl+Shift+P` → "Dev Containers: Rebuild Container"

- **Errori di compilazione dell'applicazione?**
  - Assicurati di essere nella directory corretta: `02-SetupDevEnvironment/src/github-models`
  - Prova a pulire e ricostruire: `mvn clean compile`

> **Hai bisogno di aiuto?**: Hai ancora problemi? Apri un problema nel repository e ti aiuteremo.

**Disclaimer**:  
Questo documento è stato tradotto utilizzando il servizio di traduzione automatica [Co-op Translator](https://github.com/Azure/co-op-translator). Sebbene ci impegniamo per garantire l'accuratezza, si prega di notare che le traduzioni automatiche possono contenere errori o imprecisioni. Il documento originale nella sua lingua nativa dovrebbe essere considerato la fonte autorevole. Per informazioni critiche, si raccomanda una traduzione professionale effettuata da un traduttore umano. Non siamo responsabili per eventuali fraintendimenti o interpretazioni errate derivanti dall'uso di questa traduzione.