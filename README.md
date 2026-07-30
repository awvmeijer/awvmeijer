<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/awvmeijer/awvmeijer/main/assets/banner-animated-dark.svg">
    <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/awvmeijer/awvmeijer/main/assets/banner-animated-light.svg">
    <img alt="Anthony Meijer, AI and Systems Engineer" src="https://raw.githubusercontent.com/awvmeijer/awvmeijer/main/assets/banner-animated-dark.svg" width="100%">
  </picture>
</p>

<p align="center">
  <a href="https://anthonymeijerdev.vercel.app"><code>PORTFOLIO</code></a>
  <a href="https://www.linkedin.com/in/anthonymeijer"><code>LINKEDIN</code></a>
  <a href="mailto:awvmeijer@gmail.com"><code>EMAIL</code></a>
</p>

---

I ship production AI end to end: LLM agents with persistent memory and retrieval, real-time sensor-fusion pipelines, and the detection models that decide when to act. I move comfortably from deriving a method to operating the system that runs it in production, and from model internals to a clear explanation for whoever has to trust the output.

Currently building atmospheric-intelligence systems at NTU's Earth Observatory of Singapore.

### What I work on

- **LLM agents &amp; RAG**: persistent memory, vector retrieval, knowledge graphs, agent orchestration, human-in-the-loop approval
- **Real-time ML systems**: sensor fusion, detection models, event-sourced pipelines, reproducible deployments
- **Full-stack delivery**: FastAPI and Python backends, Next.js / TypeScript frontends, PostgreSQL, containers and CI

### Selected work

<table>
  <tr>
    <td width="50%" valign="top">
      <a href="https://anthonymeijerdev.vercel.app/case-study"><img src="https://raw.githubusercontent.com/awvmeijer/awvmeijer/main/assets/shot-detector.png" alt="3DREAMS@SG" width="100%"></a>
      <br><b><code>01</code>&nbsp; 3DREAMS@SG</b> · real-time atmospheric-intelligence platform. Fuses four data sources across three LiDAR sites, scores transport episodes with a six-component model, alerts over Teams / Telegram.
      <br><sub>Python &middot; PostgreSQL &middot; Next.js &middot; Three.js</sub>
    </td>
    <td width="50%" valign="top">
      <img src="https://raw.githubusercontent.com/awvmeijer/awvmeijer/main/assets/shot-brains.png" alt="Brains" width="100%">
      <br><b><code>02</code>&nbsp; Brains</b> · self-hosted LLM agent platform: episodic memory, a live knowledge graph, and a scheduled agent fleet behind approval gates.
      <br><sub>FastAPI &middot; RAG &middot; vector search &middot; d3</sub>
    </td>
  </tr>
  <tr>
    <td width="50%" valign="top">
      <img src="https://raw.githubusercontent.com/awvmeijer/awvmeijer/main/assets/shot-forge.png" alt="Forge" width="100%">
      <br><b><code>03</code>&nbsp; Forge</b> <sub>(in development)</sub> · market-intelligence system built on Brain memory, with glass-box provenance on every claim.
      <br><sub>FastAPI &middot; DuckDB &middot; LLM</sub>
    </td>
    <td width="50%" valign="top">
      <img src="https://raw.githubusercontent.com/awvmeijer/awvmeijer/main/assets/shot-traffic.png" alt="Traffic emissions" width="100%">
      <br><b><code>04</code>&nbsp; Traffic emissions</b> · camera-based vehicle detection into a MOVES emissions model, validated against LTA reference sensors.
      <br><sub>Python &middot; computer vision &middot; MOVES</sub>
    </td>
  </tr>
  <tr>
    <td width="50%" valign="top">
      <img src="https://raw.githubusercontent.com/awvmeijer/awvmeijer/main/assets/shot-aqi.png" alt="Air-quality forecasting" width="100%">
      <br><b><code>05</code>&nbsp; Air-quality forecasting</b> · PyTorch deep net forecasting carbon-monoxide from satellite remote-sensing data.
      <br><sub>PyTorch &middot; remote sensing</sub>
    </td>
    <td width="50%" valign="top" align="center">
      <br><br><br>
      <a href="https://anthonymeijerdev.vercel.app"><b>Full case studies &amp; live demos&nbsp;&rarr;</b></a>
      <br><sub>anthonymeijer.dev</sub>
    </td>
  </tr>
</table>

> Several of these run as private production systems. Public, showcase-only versions and write-ups live in the pinned repositories and on my <a href="https://anthonymeijerdev.vercel.app">portfolio</a>.

### How 3DREAMS@SG works

Four data sources onto one clock, across three sites, on a ten-minute cycle. Every two-hour window runs two detection stages through a single scorer shared by the live pipeline, the replay engine, and the dashboard.

```mermaid
%%{init:{'theme':'base','themeVariables':{'background':'transparent','primaryColor':'transparent','secondaryColor':'transparent','tertiaryColor':'transparent','primaryBorderColor':'#8a8a85','secondaryBorderColor':'#7fd6a8','tertiaryBorderColor':'#8a8a85','primaryTextColor':'#8a8a85','secondaryTextColor':'#7fd6a8','tertiaryTextColor':'#8a8a85','lineColor':'#8a8a85','fontSize':'13px'}}}%%
flowchart LR
  L["Doppler LiDAR<br/>backscatter + wind"] --> FUSE
  AQ["NEA air quality"] --> FUSE
  FIRE["Satellite fire detections"] --> FUSE
  CLOUD["Cloud mask"] --> FUSE

  FUSE["Fusion<br/>3 sites · one clock · 10 min"] --> LEDGER[("Episode ledger<br/>replayable")]
  FUSE --> SCORE

  SCORE["Shared scorer<br/>2-hour window"] --> P["6-component probability model<br/>+ diurnal boundary-layer breakthrough"]
  SCORE --> C["3-stage cloud classifier"]

  P --> ACT
  C --> ACT
  ACT["Teams + Telegram agents · 17 commands<br/>10-panel mission control · 5-viewport geospatial hub"]

  LEDGER -.-> SCORE

  style FUSE stroke:#7fd6a8,stroke-width:1.5px
  style SCORE stroke:#7fd6a8,stroke-width:1.5px
  style ACT stroke:#7fd6a8,stroke-width:1.5px
  style LEDGER stroke:#7fd6a8,stroke-width:1.5px
```

### How Brains works

Every interaction (chat, voice, commits, mail) is embedded into an episodic memory and distilled by a model into a live knowledge graph. A scheduled agent fleet acts on that memory, and nothing outward happens without passing a human-in-the-loop gate.

```mermaid
%%{init:{'theme':'base','themeVariables':{'background':'transparent','primaryColor':'transparent','secondaryColor':'transparent','tertiaryColor':'transparent','primaryBorderColor':'#8a8a85','secondaryBorderColor':'#7fd6a8','tertiaryBorderColor':'#8a8a85','primaryTextColor':'#8a8a85','secondaryTextColor':'#7fd6a8','tertiaryTextColor':'#8a8a85','lineColor':'#8a8a85','fontSize':'13px'}}}%%
flowchart LR
  IN["Interactions<br/>chat · voice · commits · mail"] --> EMB["Embeddings<br/>vector store"]
  EMB --> MEM[("Episodic memory<br/>200K+ episodes")]
  MEM --> KG["Knowledge graph<br/>LLM-distilled entities + relations"]
  MEM --> RET["Retrieval<br/>semantic search"]
  KG --> FLEET
  RET --> FLEET
  FLEET["Scheduled agent fleet<br/>briefing · triage · reflection"] --> GATE{"Human-in-the-loop<br/>approval gate"}
  GATE --> ACT2["Actions<br/>briefings · summaries · replies"]
  ACT2 -.-> IN

  style MEM stroke:#7fd6a8,stroke-width:1.5px
  style FLEET stroke:#7fd6a8,stroke-width:1.5px
  style GATE stroke:#7fd6a8,stroke-width:1.5px
```

### Toolbox

`Python` &middot; `PyTorch` &middot; `LLM agents / RAG` &middot; `FastAPI` &middot; `PostgreSQL` &middot; `DuckDB` &middot; `TypeScript` &middot; `Next.js` &middot; `Three.js` &middot; `Docker` &middot; `Vercel / Render / Azure`

### Stats

<p>
  <img height="160" alt="GitHub stats" src="https://github-readme-stats.vercel.app/api?username=awvmeijer&show_icons=true&hide_border=false&border_color=1b1b19&bg_color=0d0e0f&title_color=7fd6a8&icon_color=7fd6a8&text_color=cfcfca">
  <img height="160" alt="Top languages" src="https://github-readme-stats.vercel.app/api/top-langs/?username=awvmeijer&layout=compact&langs_count=8&hide_border=false&border_color=1b1b19&bg_color=0d0e0f&title_color=7fd6a8&text_color=cfcfca">
</p>

<p align="center"><i>Open to AI engineering roles. The best overview is my <a href="https://anthonymeijerdev.vercel.app">portfolio</a>.</i></p>
