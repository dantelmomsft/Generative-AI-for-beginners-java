<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "2289320a74aeca1eb844cd7d3a7a9e12",
  "translation_date": "2025-07-21T19:41:49+00:00",
  "source_file": "02-SetupDevEnvironment/src/basic-chat-azure/README.md",
  "language_code": "id"
}
-->
# Obrolan Dasar dengan Azure OpenAI - Contoh End-to-End

Contoh ini menunjukkan cara membuat aplikasi Spring Boot sederhana yang terhubung ke Azure OpenAI dan menguji pengaturannya.

## Daftar Isi

- [Prasyarat](../../../../../02-SetupDevEnvironment/src/basic-chat-azure)
- [Panduan Cepat](../../../../../02-SetupDevEnvironment/src/basic-chat-azure)
- [Opsi Konfigurasi](../../../../../02-SetupDevEnvironment/src/basic-chat-azure)
  - [Opsi 1: Variabel Lingkungan (file .env) - Direkomendasikan](../../../../../02-SetupDevEnvironment/src/basic-chat-azure)
  - [Opsi 2: Rahasia GitHub Codespace](../../../../../02-SetupDevEnvironment/src/basic-chat-azure)
- [Menjalankan Aplikasi](../../../../../02-SetupDevEnvironment/src/basic-chat-azure)
  - [Menggunakan Maven](../../../../../02-SetupDevEnvironment/src/basic-chat-azure)
  - [Menggunakan VS Code](../../../../../02-SetupDevEnvironment/src/basic-chat-azure)
  - [Output yang Diharapkan](../../../../../02-SetupDevEnvironment/src/basic-chat-azure)
- [Referensi Konfigurasi](../../../../../02-SetupDevEnvironment/src/basic-chat-azure)
  - [Variabel Lingkungan](../../../../../02-SetupDevEnvironment/src/basic-chat-azure)
  - [Konfigurasi Spring](../../../../../02-SetupDevEnvironment/src/basic-chat-azure)
- [Pemecahan Masalah](../../../../../02-SetupDevEnvironment/src/basic-chat-azure)
  - [Masalah Umum](../../../../../02-SetupDevEnvironment/src/basic-chat-azure)
  - [Mode Debug](../../../../../02-SetupDevEnvironment/src/basic-chat-azure)
- [Langkah Selanjutnya](../../../../../02-SetupDevEnvironment/src/basic-chat-azure)
- [Sumber Daya](../../../../../02-SetupDevEnvironment/src/basic-chat-azure)

## Prasyarat

Sebelum menjalankan contoh ini, pastikan Anda telah:

- Menyelesaikan [panduan pengaturan Azure OpenAI](../../getting-started-azure-openai.md)  
- Mendeploy sumber daya Azure OpenAI (melalui portal Azure AI Foundry)  
- Mendeploy model gpt-4o-mini (atau alternatif lainnya)  
- Memiliki kunci API dan URL endpoint dari Azure  

## Panduan Cepat

```bash
# 1. Navigate to project
cd 02-SetupDevEnvironment/src/basic-chat-azure

# 2. Configure credentials
cp .env.example .env
# Edit .env with your Azure OpenAI credentials

# 3. Run the application
mvn spring-boot:run
```

## Opsi Konfigurasi

### Opsi 1: Variabel Lingkungan (file .env) - Direkomendasikan

**Langkah 1: Buat file konfigurasi Anda**  
```bash
cp .env.example .env
```

**Langkah 2: Tambahkan kredensial Azure OpenAI Anda**  
```bash
# Your Azure OpenAI API key (from Azure AI Foundry portal)
AZURE_AI_KEY=your-actual-api-key-here

# Your Azure OpenAI endpoint URL (e.g., https://your-hub-name.openai.azure.com/)
AZURE_AI_ENDPOINT=https://your-hub-name.openai.azure.com/
```

> **Catatan Keamanan**:  
> - Jangan pernah mengunggah file `.env` Anda ke sistem kontrol versi  
> - File `.env` sudah ada dalam `.gitignore`  
> - Jaga keamanan kunci API Anda dan lakukan rotasi secara berkala  

### Opsi 2: Rahasia GitHub Codespace

Untuk GitHub Codespaces, atur rahasia ini di repositori Anda:  
- `AZURE_AI_KEY` - Kunci API Azure OpenAI Anda  
- `AZURE_AI_ENDPOINT` - URL endpoint Azure OpenAI Anda  

Aplikasi akan secara otomatis mendeteksi dan menggunakan rahasia ini.

### Alternatif: Variabel Lingkungan Langsung

<details>
<summary>Klik untuk melihat perintah spesifik platform</summary>

**Linux/macOS (bash/zsh):**  
```bash
export AZURE_AI_KEY=your-actual-api-key-here
export AZURE_AI_ENDPOINT=https://your-hub-name.openai.azure.com/
```

**Windows (Command Prompt):**  
```cmd
set AZURE_AI_KEY=your-actual-api-key-here
set AZURE_AI_ENDPOINT=https://your-hub-name.openai.azure.com/
```

**Windows (PowerShell):**  
```powershell
$env:AZURE_AI_KEY="your-actual-api-key-here"
$env:AZURE_AI_ENDPOINT="https://your-hub-name.openai.azure.com/"
```
</details>

## Menjalankan Aplikasi

### Menggunakan Maven

```bash
mvn spring-boot:run
```

### Menggunakan VS Code

1. Buka proyek di VS Code  
2. Tekan `F5` atau gunakan panel "Run and Debug"  
3. Pilih konfigurasi "Spring Boot-BasicChatApplication"  

> **Catatan**: Konfigurasi VS Code secara otomatis memuat file .env Anda  

### Output yang Diharapkan

```
Starting Basic Chat with Azure OpenAI...
Environment variables loaded successfully
Connecting to Azure OpenAI...
Sending prompt: What is AI in a short sentence? Max 100 words.

AI Response:
================
AI, or Artificial Intelligence, is the simulation of human intelligence in machines programmed to think and learn like humans.
================

Success! Azure OpenAI connection is working correctly.
```

## Referensi Konfigurasi

### Variabel Lingkungan

| Variabel | Deskripsi | Wajib | Contoh |
|----------|-----------|-------|--------|
| `AZURE_AI_KEY` | Kunci API Azure OpenAI | Ya | `abc123...` |
| `AZURE_AI_ENDPOINT` | URL endpoint Azure OpenAI | Ya | `https://my-hub.openai.azure.com/` |
| `AZURE_AI_MODEL_DEPLOYMENT` | Nama deployment model | Tidak | `gpt-4o-mini` (default) |

### Konfigurasi Spring

File `application.yml` mengatur:  
- **Kunci API**: `${AZURE_AI_KEY}` - Dari variabel lingkungan  
- **Endpoint**: `${AZURE_AI_ENDPOINT}` - Dari variabel lingkungan  
- **Model**: `${AZURE_AI_MODEL_DEPLOYMENT:gpt-4o-mini}` - Dari variabel lingkungan dengan fallback  
- **Temperature**: `0.7` - Mengontrol kreativitas (0.0 = deterministik, 1.0 = kreatif)  
- **Max Tokens**: `500` - Panjang respons maksimum  

## Pemecahan Masalah

### Masalah Umum

<details>
<summary><strong>Kesalahan: "The API key is not valid"</strong></summary>

- Periksa apakah `AZURE_AI_KEY` Anda sudah diatur dengan benar di file `.env`  
- Pastikan kunci API disalin persis dari portal Azure AI Foundry  
- Pastikan tidak ada spasi atau tanda kutip tambahan di sekitar kunci  
</details>

<details>
<summary><strong>Kesalahan: "The endpoint is not valid"</strong></summary>

- Pastikan `AZURE_AI_ENDPOINT` Anda mencakup URL lengkap (misalnya, `https://your-hub-name.openai.azure.com/`)  
- Periksa konsistensi tanda garis miring di akhir URL  
- Pastikan endpoint sesuai dengan wilayah deployment Azure Anda  
</details>

<details>
<summary><strong>Kesalahan: "The deployment was not found"</strong></summary>

- Pastikan nama deployment model Anda sesuai persis dengan yang dideploy di Azure  
- Periksa apakah model berhasil dideploy dan aktif  
- Coba gunakan nama deployment default: `gpt-4o-mini`  
</details>

<details>
<summary><strong>VS Code: Variabel lingkungan tidak dimuat</strong></summary>

- Pastikan file `.env` Anda ada di direktori root proyek (level yang sama dengan `pom.xml`)  
- Coba jalankan `mvn spring-boot:run` di terminal terintegrasi VS Code  
- Periksa apakah ekstensi Java VS Code sudah terinstal dengan benar  
- Verifikasi konfigurasi peluncuran memiliki `"envFile": "${workspaceFolder}/.env"`  
</details>

### Mode Debug

Untuk mengaktifkan logging yang lebih rinci, hapus komentar pada baris berikut di `application.yml`:

```yaml
logging:
  level:
    org.springframework.ai: DEBUG
    com.azure: DEBUG
```

## Langkah Selanjutnya

**Pengaturan Selesai!** Lanjutkan perjalanan pembelajaran Anda:

[Chapter 3: Core Generative AI Techniques](../../../03-CoreGenerativeAITechniques/README.md)

## Sumber Daya

- [Dokumentasi Spring AI Azure OpenAI](https://docs.spring.io/spring-ai/reference/api/clients/azure-openai-chat.html)  
- [Dokumentasi Layanan Azure OpenAI](https://learn.microsoft.com/azure/ai-services/openai/)  
- [Portal Azure AI Foundry](https://ai.azure.com/)  
- [Dokumentasi Azure AI Foundry](https://learn.microsoft.com/azure/ai-foundry/how-to/create-projects?tabs=ai-foundry&pivots=hub-project)  

**Penafian**:  
Dokumen ini telah diterjemahkan menggunakan layanan penerjemahan AI [Co-op Translator](https://github.com/Azure/co-op-translator). Meskipun kami berusaha untuk memberikan terjemahan yang akurat, harap diingat bahwa terjemahan otomatis mungkin mengandung kesalahan atau ketidakakuratan. Dokumen asli dalam bahasa aslinya harus dianggap sebagai sumber yang otoritatif. Untuk informasi yang bersifat kritis, disarankan menggunakan jasa penerjemahan profesional oleh manusia. Kami tidak bertanggung jawab atas kesalahpahaman atau penafsiran yang keliru yang timbul dari penggunaan terjemahan ini.