<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "df269f529a172a0197ef28460bf1da9f",
  "translation_date": "2025-07-25T10:49:00+00:00",
  "source_file": "04-PracticalSamples/README.md",
  "language_code": "ur"
}
-->
# عملی اطلاقات اور منصوبے

## آپ کیا سیکھیں گے
اس سیکشن میں ہم تین عملی اطلاقات کا مظاہرہ کریں گے جو جاوا کے ساتھ جنریٹو AI ترقی کے نمونے پیش کرتے ہیں:
- کلائنٹ سائیڈ اور سرور سائیڈ AI کو ملا کر ایک ملٹی موڈل پالتو کہانی جنریٹر بنائیں
- فاؤنڈری لوکل اسپرنگ بوٹ ڈیمو کے ساتھ مقامی AI ماڈل انضمام نافذ کریں
- کیلکولیٹر مثال کے ساتھ ایک ماڈل کانٹیکسٹ پروٹوکول (MCP) سروس تیار کریں

## مواد کی فہرست

- [تعارف](../../../04-PracticalSamples)
  - [فاؤنڈری لوکل اسپرنگ بوٹ ڈیمو](../../../04-PracticalSamples)
  - [پالتو کہانی جنریٹر](../../../04-PracticalSamples)
  - [MCP کیلکولیٹر سروس (ابتدائی دوستانہ MCP ڈیمو)](../../../04-PracticalSamples)
- [سیکھنے کی ترقی](../../../04-PracticalSamples)
- [خلاصہ](../../../04-PracticalSamples)
- [اگلے اقدامات](../../../04-PracticalSamples)

## تعارف

یہ باب **نمونہ منصوبے** پیش کرتا ہے جو جاوا کے ساتھ جنریٹو AI ترقی کے نمونے دکھاتے ہیں۔ ہر منصوبہ مکمل طور پر فعال ہے اور مخصوص AI ٹیکنالوجیز، آرکیٹیکچرل نمونے، اور بہترین طریقے پیش کرتا ہے جنہیں آپ اپنی ایپلیکیشنز کے لیے اپنانا چاہتے ہیں۔

### فاؤنڈری لوکل اسپرنگ بوٹ ڈیمو

**[فاؤنڈری لوکل اسپرنگ بوٹ ڈیمو](foundrylocal/README.md)** دکھاتا ہے کہ **OpenAI Java SDK** کا استعمال کرتے ہوئے مقامی AI ماڈلز کے ساتھ انضمام کیسے کیا جائے۔ یہ **Phi-3.5-mini** ماڈل سے جڑنے کا مظاہرہ کرتا ہے جو فاؤنڈری لوکل پر چل رہا ہے، جس سے آپ AI ایپلیکیشنز کو کلاؤڈ سروسز پر انحصار کیے بغیر چلا سکتے ہیں۔

### پالتو کہانی جنریٹر

**[پالتو کہانی جنریٹر](petstory/README.md)** ایک دلچسپ اسپرنگ بوٹ ویب ایپلیکیشن ہے جو **ملٹی موڈل AI پروسیسنگ** کا مظاہرہ کرتی ہے تاکہ تخلیقی پالتو کہانیاں بنائی جا سکیں۔ یہ کلائنٹ سائیڈ اور سرور سائیڈ AI صلاحیتوں کو یکجا کرتا ہے، جس میں براؤزر پر مبنی AI تعاملات کے لیے transformer.js اور سرور سائیڈ پروسیسنگ کے لیے OpenAI SDK استعمال ہوتا ہے۔

### MCP کیلکولیٹر سروس (ابتدائی دوستانہ MCP ڈیمو)

**[MCP کیلکولیٹر سروس](mcp/calculator/README.md)** **ماڈل کانٹیکسٹ پروٹوکول (MCP)** کا ایک سادہ مظاہرہ ہے جو اسپرنگ AI کا استعمال کرتا ہے۔ یہ MCP تصورات کا ایک ابتدائی دوستانہ تعارف فراہم کرتا ہے، جس میں دکھایا گیا ہے کہ ایک بنیادی MCP سرور کیسے بنایا جائے جو MCP کلائنٹس کے ساتھ تعامل کرتا ہے۔

## سیکھنے کی ترقی

یہ منصوبے پچھلے ابواب کے تصورات پر مبنی ہیں:

1. **سادہ سے شروع کریں**: فاؤنڈری لوکل اسپرنگ بوٹ ڈیمو کے ساتھ شروع کریں تاکہ مقامی ماڈلز کے ساتھ بنیادی AI انضمام کو سمجھا جا سکے
2. **تفاعل شامل کریں**: پالتو کہانی جنریٹر کی طرف بڑھیں تاکہ ملٹی موڈل AI اور ویب پر مبنی تعاملات کو سمجھا جا سکے
3. **MCP بنیادی باتیں سیکھیں**: MCP کیلکولیٹر سروس آزمائیں تاکہ ماڈل کانٹیکسٹ پروٹوکول کی بنیادی باتیں سمجھ سکیں

## خلاصہ

**مبارک ہو!** آپ نے کامیابی سے:

- **ملٹی موڈل AI تجربات تخلیق کیے** جو کلائنٹ سائیڈ اور سرور سائیڈ AI پروسیسنگ کو یکجا کرتے ہیں
- **مقامی AI ماڈل انضمام نافذ کیا** جدید جاوا فریم ورک اور SDKs کا استعمال کرتے ہوئے
- **ماڈل کانٹیکسٹ پروٹوکول سروسز تیار کیں** جو ٹول انضمام کے نمونے دکھاتی ہیں

## اگلے اقدامات

[باب 5: ذمہ دار جنریٹو AI](../05-ResponsibleGenAI/README.md)

**ڈسکلیمر**:  
یہ دستاویز AI ترجمہ سروس [Co-op Translator](https://github.com/Azure/co-op-translator) کا استعمال کرتے ہوئے ترجمہ کی گئی ہے۔ ہم درستگی کے لیے کوشش کرتے ہیں، لیکن براہ کرم آگاہ رہیں کہ خودکار ترجمے میں غلطیاں یا غیر درستیاں ہو سکتی ہیں۔ اصل دستاویز کو اس کی اصل زبان میں مستند ذریعہ سمجھا جانا چاہیے۔ اہم معلومات کے لیے، پیشہ ور انسانی ترجمہ کی سفارش کی جاتی ہے۔ ہم اس ترجمے کے استعمال سے پیدا ہونے والی کسی بھی غلط فہمی یا غلط تشریح کے ذمہ دار نہیں ہیں۔