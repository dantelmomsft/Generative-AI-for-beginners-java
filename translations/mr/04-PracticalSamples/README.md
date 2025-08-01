<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "df269f529a172a0197ef28460bf1da9f",
  "translation_date": "2025-07-25T11:06:41+00:00",
  "source_file": "04-PracticalSamples/README.md",
  "language_code": "mr"
}
-->
# व्यावहारिक उपयोग आणि प्रकल्प

## तुम्ही काय शिकाल
या विभागात आम्ही तीन व्यावहारिक अनुप्रयोगांचे प्रात्यक्षिक दाखवू जे Java सह जनरेटिव्ह AI विकास पद्धती दर्शवतात:
- क्लायंट-साइड आणि सर्व्हर-साइड AI एकत्रित करून मल्टी-मोडल Pet Story Generator तयार करा
- Foundry Local Spring Boot डेमोसह स्थानिक AI मॉडेल एकत्रीकरण अंमलात आणा
- Calculator उदाहरणासह Model Context Protocol (MCP) सेवा विकसित करा

## विषय सूची

- [परिचय](../../../04-PracticalSamples)
  - [Foundry Local Spring Boot डेमो](../../../04-PracticalSamples)
  - [Pet Story Generator](../../../04-PracticalSamples)
  - [MCP Calculator सेवा (सोप्या MCP डेमो)](../../../04-PracticalSamples)
- [शिकण्याची प्रगती](../../../04-PracticalSamples)
- [सारांश](../../../04-PracticalSamples)
- [पुढील पायऱ्या](../../../04-PracticalSamples)

## परिचय

या प्रकरणात **नमुन्याचे प्रकल्प** दाखवले आहेत जे Java सह जनरेटिव्ह AI विकास पद्धती दर्शवतात. प्रत्येक प्रकल्प पूर्णपणे कार्यक्षम आहे आणि विशिष्ट AI तंत्रज्ञान, आर्किटेक्चरल पद्धती आणि सर्वोत्तम पद्धती दर्शवतो, ज्याचा तुम्ही तुमच्या स्वतःच्या अनुप्रयोगांसाठी उपयोग करू शकता.

### Foundry Local Spring Boot डेमो

**[Foundry Local Spring Boot डेमो](foundrylocal/README.md)** स्थानिक AI मॉडेलसह **OpenAI Java SDK** वापरून एकत्रीकरण कसे करायचे ते दाखवते. हे **Phi-3.5-mini** मॉडेलशी कनेक्ट होण्याचे प्रात्यक्षिक देते जे Foundry Local वर चालते, ज्यामुळे तुम्ही क्लाउड सेवांवर अवलंबून न राहता AI अनुप्रयोग चालवू शकता.

### Pet Story Generator

**[Pet Story Generator](petstory/README.md)** एक आकर्षक Spring Boot वेब अनुप्रयोग आहे जो **मल्टी-मोडल AI प्रक्रिया** दाखवतो ज्याद्वारे सर्जनशील पाळीव प्राणी कथा तयार करता येतात. हे ब्राउझर-आधारित AI संवादांसाठी transformer.js आणि सर्व्हर-साइड प्रक्रियेसाठी OpenAI SDK वापरून क्लायंट-साइड आणि सर्व्हर-साइड AI क्षमता एकत्रित करते.

### MCP Calculator सेवा (सोप्या MCP डेमो)

**[MCP Calculator सेवा](mcp/calculator/README.md)** **Model Context Protocol (MCP)** चा Spring AI वापरून एक साधा प्रात्यक्षिक आहे. हे MCP संकल्पनांचे सुरुवातीसाठी अनुकूल परिचय देते, ज्यामध्ये MCP Server तयार करणे आणि MCP क्लायंट्सशी संवाद साधणे कसे करायचे ते दाखवले आहे.

## शिकण्याची प्रगती

हे प्रकल्प मागील प्रकरणांतील संकल्पनांवर आधारित तयार केले आहेत:

1. **सोप्या गोष्टींनी सुरुवात करा**: Foundry Local Spring Boot डेमोने सुरुवात करा जे स्थानिक मॉडेलसह मूलभूत AI एकत्रीकरण समजून घेण्यासाठी आहे
2. **परस्परसंवाद जोडा**: Pet Story Generator वापरून मल्टी-मोडल AI आणि वेब-आधारित संवादांसाठी प्रगती करा
3. **MCP मूलभूत गोष्टी शिका**: Model Context Protocol च्या मूलभूत गोष्टी समजून घेण्यासाठी MCP Calculator सेवा वापरून पहा

## सारांश

**अभिनंदन!** तुम्ही यशस्वीरित्या:

- **मल्टी-मोडल AI अनुभव तयार केले** ज्यामध्ये क्लायंट-साइड आणि सर्व्हर-साइड AI प्रक्रिया एकत्रित केली आहे
- **स्थानिक AI मॉडेल एकत्रीकरण अंमलात आणले** आधुनिक Java फ्रेमवर्क आणि SDK वापरून
- **Model Context Protocol सेवा विकसित केल्या** ज्यामध्ये टूल एकत्रीकरण पद्धतींचे प्रात्यक्षिक दिले आहे

## पुढील पायऱ्या

[प्रकरण 5: जबाबदार जनरेटिव्ह AI](../05-ResponsibleGenAI/README.md)

**अस्वीकरण**:  
हा दस्तऐवज AI भाषांतर सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) वापरून भाषांतरित करण्यात आला आहे. आम्ही अचूकतेसाठी प्रयत्नशील असलो तरी कृपया लक्षात ठेवा की स्वयंचलित भाषांतरे त्रुटी किंवा अचूकतेच्या अभावाने युक्त असू शकतात. मूळ भाषेतील दस्तऐवज हा अधिकृत स्रोत मानला जावा. महत्त्वाच्या माहितीसाठी व्यावसायिक मानवी भाषांतराची शिफारस केली जाते. या भाषांतराचा वापर करून उद्भवलेल्या कोणत्याही गैरसमज किंवा चुकीच्या अर्थासाठी आम्ही जबाबदार नाही.