<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "df269f529a172a0197ef28460bf1da9f",
  "translation_date": "2025-07-25T11:26:51+00:00",
  "source_file": "04-PracticalSamples/README.md",
  "language_code": "th"
}
-->
# การประยุกต์ใช้งานจริงและโปรเจกต์

## สิ่งที่คุณจะได้เรียนรู้
ในส่วนนี้ เราจะสาธิตการประยุกต์ใช้งานจริง 3 ตัวอย่างที่แสดงรูปแบบการพัฒนา AI เชิงสร้างสรรค์ด้วย Java:
- สร้างตัวสร้างเรื่องราวสัตว์เลี้ยงแบบหลายรูปแบบ (multi-modal) ที่ผสมผสาน AI ฝั่งไคลเอนต์และเซิร์ฟเวอร์
- ใช้งานการผสานรวมโมเดล AI ในเครื่องด้วย Foundry Local Spring Boot Demo
- พัฒนาบริการ Model Context Protocol (MCP) ด้วยตัวอย่างเครื่องคิดเลข

## สารบัญ

- [บทนำ](../../../04-PracticalSamples)
  - [Foundry Local Spring Boot Demo](../../../04-PracticalSamples)
  - [ตัวสร้างเรื่องราวสัตว์เลี้ยง](../../../04-PracticalSamples)
  - [บริการ MCP เครื่องคิดเลข (ตัวอย่าง MCP สำหรับผู้เริ่มต้น)](../../../04-PracticalSamples)
- [ลำดับการเรียนรู้](../../../04-PracticalSamples)
- [สรุป](../../../04-PracticalSamples)
- [ขั้นตอนถัดไป](../../../04-PracticalSamples)

## บทนำ

บทนี้แสดงตัวอย่างโปรเจกต์ที่ **ใช้งานได้จริง** ซึ่งแสดงรูปแบบการพัฒนา AI เชิงสร้างสรรค์ด้วย Java แต่ละโปรเจกต์สามารถทำงานได้อย่างสมบูรณ์และแสดงเทคโนโลยี AI เฉพาะทาง รูปแบบสถาปัตยกรรม และแนวปฏิบัติที่ดีที่สุดที่คุณสามารถนำไปปรับใช้กับแอปพลิเคชันของคุณเอง

### Foundry Local Spring Boot Demo

**[Foundry Local Spring Boot Demo](foundrylocal/README.md)** แสดงวิธีการผสานรวมกับโมเดล AI ในเครื่องโดยใช้ **OpenAI Java SDK** ตัวอย่างนี้แสดงการเชื่อมต่อกับโมเดล **Phi-3.5-mini** ที่ทำงานบน Foundry Local ซึ่งช่วยให้คุณสามารถใช้งานแอปพลิเคชัน AI ได้โดยไม่ต้องพึ่งพาบริการคลาวด์

### ตัวสร้างเรื่องราวสัตว์เลี้ยง

**[ตัวสร้างเรื่องราวสัตว์เลี้ยง](petstory/README.md)** เป็นแอปพลิเคชันเว็บ Spring Boot ที่น่าสนใจ ซึ่งแสดงการประมวลผล AI แบบ **หลายรูปแบบ (multi-modal)** เพื่อสร้างเรื่องราวสัตว์เลี้ยงที่สร้างสรรค์ โดยผสมผสานความสามารถของ AI ฝั่งไคลเอนต์และเซิร์ฟเวอร์ผ่าน transformer.js สำหรับการโต้ตอบ AI บนเบราว์เซอร์ และ OpenAI SDK สำหรับการประมวลผลฝั่งเซิร์ฟเวอร์

### บริการ MCP เครื่องคิดเลข (ตัวอย่าง MCP สำหรับผู้เริ่มต้น)

**[บริการ MCP เครื่องคิดเลข](mcp/calculator/README.md)** เป็นตัวอย่างง่าย ๆ ของ **Model Context Protocol (MCP)** โดยใช้ Spring AI ตัวอย่างนี้เหมาะสำหรับผู้เริ่มต้นที่ต้องการเรียนรู้แนวคิด MCP โดยแสดงวิธีการสร้าง MCP Server พื้นฐานที่สามารถโต้ตอบกับ MCP Client ได้

## ลำดับการเรียนรู้

โปรเจกต์เหล่านี้ถูกออกแบบมาเพื่อสร้างความเข้าใจต่อเนื่องจากบทก่อนหน้า:

1. **เริ่มต้นแบบง่าย ๆ**: เริ่มต้นด้วย Foundry Local Spring Boot Demo เพื่อเข้าใจการผสานรวม AI เบื้องต้นกับโมเดลในเครื่อง
2. **เพิ่มการโต้ตอบ**: ต่อด้วยตัวสร้างเรื่องราวสัตว์เลี้ยงเพื่อเรียนรู้การประมวลผล AI แบบหลายรูปแบบและการโต้ตอบผ่านเว็บ
3. **เรียนรู้พื้นฐาน MCP**: ทดลองบริการ MCP เครื่องคิดเลขเพื่อเข้าใจพื้นฐานของ Model Context Protocol

## สรุป

**ยินดีด้วย!** คุณได้ประสบความสำเร็จในการ:

- **สร้างประสบการณ์ AI แบบหลายรูปแบบ** ที่ผสมผสานการประมวลผล AI ฝั่งไคลเอนต์และเซิร์ฟเวอร์
- **ใช้งานการผสานรวมโมเดล AI ในเครื่อง** โดยใช้เฟรมเวิร์กและ SDK ของ Java ที่ทันสมัย
- **พัฒนาบริการ Model Context Protocol** ที่แสดงรูปแบบการผสานรวมเครื่องมือ

## ขั้นตอนถัดไป

[บทที่ 5: AI เชิงสร้างสรรค์อย่างมีความรับผิดชอบ](../05-ResponsibleGenAI/README.md)

**ข้อจำกัดความรับผิดชอบ**:  
เอกสารนี้ได้รับการแปลโดยใช้บริการแปลภาษา AI [Co-op Translator](https://github.com/Azure/co-op-translator) แม้ว่าเราจะพยายามอย่างเต็มที่เพื่อความถูกต้อง โปรดทราบว่าการแปลอัตโนมัติอาจมีข้อผิดพลาดหรือความไม่ถูกต้อง เอกสารต้นฉบับในภาษาต้นทางควรถือเป็นแหล่งข้อมูลที่เชื่อถือได้ สำหรับข้อมูลที่สำคัญ แนะนำให้ใช้บริการแปลภาษามนุษย์ที่เป็นมืออาชีพ เราไม่รับผิดชอบต่อความเข้าใจผิดหรือการตีความที่ผิดพลาดซึ่งเกิดจากการใช้การแปลนี้