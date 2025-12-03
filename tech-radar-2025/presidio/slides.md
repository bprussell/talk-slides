---
theme: default
background: https://source.unsplash.com/collection/94734566/1920x1080
class: text-center
highlighter: shiki
lineNumbers: false
info: |
  ## Presidio
  Microsoft's open-source PII detection and anonymization framework
drawings:
  persist: false
transition: slide-left
title: 'Presidio: PII Detection & Anonymization'
mdc: true
---

# Presidio

**PII Detection & Anonymization**

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    Microsoft's Open-Source Privacy Framework
  </span>
</div>

---
layout: two-cols
---

# What is Presidio?

Microsoft's open-source PII detection, anonymization & synthesis framework

- **Detect** 50+ entity types (SSN, credit cards, names, emails, medical)
- **Anonymize** via redaction, masking, hashing, encryption
- **Synthesize** realistic replacements for detected PII
- Text and image support • Python, Docker, K8s, PySpark

::right::

<div class="mt-4">

```python
from presidio_analyzer import AnalyzerEngine
from presidio_anonymizer import AnonymizerEngine

analyzer = AnalyzerEngine()
results = analyzer.analyze(
    text="John's SSN is 123-45-6789",
    language='en'
)
print(results)
# [type: SSN, start: 16, end: 27, score: 0.85]

anonymizer = AnonymizerEngine()
anonymized = anonymizer.anonymize(
    text="John's SSN is 123-45-6789",
    analyzer_results=results
)
print(anonymized.text)
# "John's SSN is <SSN>"
```

</div>

---
layout: default
---

# Use Cases & Benefits

<div class="grid grid-cols-2 gap-8">

<div>

### Use Cases
- Sanitize LLM training data
- Privacy-compliant analytics
- Medical record redaction
- Test data with synthetic PII

</div>

<div>

### Benefits
- Open source (MIT)
- 6.3k+ GitHub stars
- Multi-language support
- Microsoft-backed

</div>

</div>

---
layout: default
---

# The Important Caveat

<div class="text-center mt-16">

<div class="text-3xl text-red-400 font-bold mb-8">
⚠️ No Guarantees
</div>

<div class="text-xl">
"Because it is using automated detection mechanisms,<br/>
there is <span class="text-red-400 font-bold">no guarantee</span> that Presidio will find<br/>
<span class="text-red-400 font-bold">all sensitive information</span>"
</div>

<div class="text-sm text-gray-500 mt-4">
— Presidio GitHub README
</div>

<div class="mt-8 text-gray-400">
→ Use as part of a defense-in-depth strategy<br/>
→ Combine with manual review for critical data<br/>
→ Regular testing and validation required
</div>

</div>

---
layout: default
---

# Alternatives in the Market

- **AWS Comprehend** - Managed PII detection service
- **Google Cloud DLP** - Data Loss Prevention API
- **Gretel.ai** - Synthetic data + PII detection
- **DataSynthesizer** - Open-source data anonymization
- **Custom NER models** - Build your own with spaCy/Hugging Face

---
layout: center
class: text-center
---

# Tech Radar: Trial

<div class="mt-8">

### Recommendation: **Trial**

<div class="mt-8 text-xl max-w-3xl mx-auto">
Great for sanitizing LLM training data, creating safe test datasets.
<br/><br/>
...but don't rely on it alone.
</div>

</div>

<div class="mt-12">

🔗 **github.com/microsoft/presidio**

</div>

---
layout: center
class: text-center
---

# Demo!
