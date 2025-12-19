---
theme: the-unnamed
background: https://source.unsplash.com/collection/94734566/1920x1080
class: text-center
highlighter: shiki
lineNumbers: false
info: |
  ## Browser Use
  AI-driven browser automation with language models
drawings:
  persist: false
transition: slide-left
title: 'Browser Use: AI-Powered Web Automation'
mdc: true
---

# Browser Use

**AI-Powered Web Automation**

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    Automate Web Tasks with Language Models
  </span>
</div>

---
layout: two-cols
---

# What is Browser Use?

Open-source Python library that lets AI agents automate web interactions through natural language

- **Navigate & interact** with websites programmatically
- **Fill forms, extract data**, perform multi-step tasks
- **Works with Claude, GPT, Gemini** and other LLMs
- **53 tasks per dollar** — 15x cheaper than competitors
- **6x faster** than standard LLM approaches

::right::

<div class="mt-4">

```python
from browser_use import Agent
from anthropic import Anthropic

agent = Agent(
    task="Find the cheapest laptop under $1000",
    llm=Anthropic(),
)

result = agent.run()
print(result)
# Visited 5 sites, found Dell XPS for $899
```

</div>

---
layout: default
---

# Use Cases & Benefits

<div class="grid grid-cols-2 gap-8">

<div>

### Use Cases
- Automated testing with natural language
- Web scraping & data extraction
- Job/form automation
- Research & price monitoring
- Integration with non-API services

</div>

<div>

### Benefits
- Open source (MIT)
- Zero DevOps overhead
- Multi-LLM support
- Stealth mode (bypass CAPTCHAs)
- Persistent sessions & profiles

</div>

</div>

---
layout: default
---

# Important Limitations

<div class="text-center mt-16">

<div class="text-3xl text-yellow-400 font-bold mb-8">
⚠️ Still Emerging Technology
</div>

<div class="text-xl">
Agent outputs can be <span class="text-yellow-400 font-bold">unreliable</span>
<br/>
Failure descriptions often <span class="text-yellow-400 font-bold">lack detail</span>
<br/>
Requires <span class="text-yellow-400 font-bold">careful error handling</span>
</div>

<div class="text-sm text-gray-500 mt-4">
— Thoughtworks Radar Assessment
</div>

<div class="mt-8 text-gray-400">
→ Works best for well-structured websites<br/>
→ Complex UIs and dynamic content still challenging<br/>
→ Manual intervention may be needed
</div>

</div>

---
layout: default
---

# Alternatives

<div class="grid grid-cols-2 gap-8">

<div>

### Traditional Automation
- **Selenium** - Mature, cross-browser
- **Playwright** - Modern, fast
- **Puppeteer** - Chrome DevTools Protocol

</div>

<div>

### AI-Powered Testing
- **testRigor** - Plain English tests, self-healing
- **Sauce Labs AutonomIQ** - AI test agent
- **Claude Computer Use** - LLM-driven browser automation

</div>

</div>

---
layout: center
class: text-center
---

# Tech Radar: Assess

<div class="mt-8">

### Recommendation: **Assess**

<div class="mt-8 text-xl max-w-3xl mx-auto">
Explore for automation use cases and integrated testing.
<br/><br/>
...but wait for output reliability to improve before production adoption.
</div>

</div>

<div class="mt-12">

🔗 **github.com/browser-use/browser-use**

</div>

---
layout: center
class: text-center
---

# Demo!
