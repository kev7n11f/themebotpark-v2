# ThemeBotPark-v2

Each top-level directory contains a README that outlines its naming conventions, file formats, and role in the overall architecture.

# ThemeBotPark

A unified, extensible platform for creating, orchestrating, and deploying themed bot experiences across web, chat, voice, and physical environments. ThemeBotPark empowers developers, designers, and content creators to build immersive, interactive “bot parks” where each bot embodies a unique aesthetic, persona, and functionality.

---

## Table of Contents

1. [Vision & Goals](#vision--goals)  
2. [Core Features](#core-features)  
3. [Architecture Overview](#architecture-overview)  
4. [Technology Stack](#technology-stack)  
5. [Getting Started](#getting-started)  
6. [Configuration & Theming](#configuration--theming)  
7. [Bot Modules & Integrations](#bot-modules--integrations)  
8. [CLI & Workflow](#cli--workflow)  
9. [Testing & CI/CD](#testing--cicd)  
10. [Roadmap](#roadmap)  
11. [Contributing](#contributing)  
12. [License & Code of Conduct](#license--code-of-conduct)  

---

## Vision & Goals

ThemeBotPark envisions a future where interactive bots are not just utilities but characters in rich, thematic worlds.  

- Enable rapid prototyping of themed bots for marketing campaigns, educational experiences, live events, and smart environments.  
- Provide a low-code, highly configurable toolkit for designers and developers to craft consistent brand experiences.  
- Allow seamless integration with messaging platforms (Slack, Discord), voice assistants (Alexa, Google Assistant), IoT devices, and web interfaces.  
- Support dynamic environment controls (lighting, sound, projection) for physical installations.  

---

## Core Features

- **Theme Templates**  
  Predefined starter kits (e.g., Noir Detective, Futuristic Tech Expo, Fantasy Tavern) with assets, dialogue flows, and environment settings.

- **Modular Bot Framework**  
  - Dialogue Module (NLP, state management)  
  - Persona Module (voice, avatar, backstory)  
  - Action Module (API calls, webhooks, IoT triggers)  

- **Multi-Channel Deployment**  
  - Chat (Slack, Discord, Microsoft Teams)  
  - Web Chat Widget  
  - Voice Assistants  
  - Physical Kiosks & Installations  

- **Environment Orchestration**  
  - Smart lighting  
  - Soundscapes  
  - Projection mapping  

- **Configuration-Driven**  
  Single JSON/YAML file defines themes, bots, channels, and environment integrations.

- **Analytics & Insights**  
  Dashboard for usage stats, sentiment analysis, and engagement metrics.

---

## Architecture Overview

```ascii
+----------------------+     +-------------------+
|  ThemeBotPark CLI    |<--->|  Config Files     |
+----------------------+     +-------------------+
           |
           v
+----------------------+     +----------------+
| Bot Orchestrator     |<--> | Theme Registry |
| (Node.js + Express)  |     +----------------+
+----------------------+
     |    |    |    |
     v    v    v    v
+-----+ +-----+ +-----+ +-----+
|Chat | |Voice| |IoT  | |Web  |
|Adapter|Adapter|Adapter|Adapter|
+-----+ +-----+ +-----+ +-----+
```

- **CLI**: scaffolds themes, deploys to cloud or local Docker, runs simulations.  
- **Orchestrator**: core runtime managing bots, channels, and environment hooks.  
- **Adapters**: implement channel-specific protocols and SDKs.  
- **Registry**: centralized store for theme metadata, versions, asset URIs.  

---

## Technology Stack

| Layer                  | Technology                         |
|------------------------|------------------------------------|
| Runtime                | Node.js (v18+)                     |
| Framework              | Express.js                         |
| CLI                    | oclif / Commander.js               |
| Messaging Adapters     | Slack SDK, Discord.js, MS Teams    |
| Voice Integrations     | Alexa SDK, Actions on Google       |
| Web Widget             | React + TypeScript                 |
| Environment Control    | MQTT / WebSockets                  |
| Configuration          | JSON5 / YAML                       |
| Testing                | Jest, Cypress                      |
| CI/CD                  | GitHub Actions, Docker, Kubernetes |
| Analytics              | Grafana, Prometheus                |

---

## Getting Started

### Prerequisites

- Node.js v18+  
- Docker & Docker Compose (for local environment)  
- Access credentials for target channels (Slack app tokens, Alexa skill IDs, etc.)  

### Installation

```bash
git clone https://github.com/your-org/themebotpark.git
cd themebotpark
npm install
```

### Configuration

1. Copy the sample config:  
   ```bash
   cp config/themebotpark.example.json config/themebotpark.json
   ```
2. Edit `config/themebotpark.json` with your theme, bots, and channels.  
3. Define credentials in `~/.themebotpark/credentials.json` or via environment variables.

### Running Locally

```bash
npm run dev            # starts Orchestrator + Web Dashboard
npm run cli -- deploy  # deploys bots to local Docker Compose
```

---

## Configuration & Theming

### Sample `themebotpark.json`

```json5
{
  "theme": {
    "id": "futuristic-expo",
    "name": "Futuristic Tech Expo",
    "assets": {
      "avatarBaseUrl": "https://cdn.example.com/themes/futuristic-expo/avatars/",
      "soundscape": "https://cdn.example.com/themes/futuristic-expo/sounds/ambience.mp3"
    },
    "environment": {
      "lighting": { "mode": "neon-blue", "controller": "mqtt://192.168.0.50" },
      "projector": { "slides": [ "slide1.jpg","slide2.jpg" ] }
    }
  },
  "bots": [
    {
      "id": "expo-guide",
      "persona": { "voice": "alex", "avatar": "guide.png", "backstory": "Your friendly expo guide." },
      "dialogue": "bots/expo-guide/flow.dialogue",
      "actions": [
        { "trigger": "show_slide", "type": "projector.slide", "payloadKey": "slide" }
      ]
    }
  ],
  "channels": [
    { "type": "slack", "token": "${SLACK_TOKEN}", "botId": "expo-guide" },
    { "type": "webwidget", "path": "/chat" }
  ]
}
```

### Creating a New Theme

1. `themebotpark-cli scaffold theme <theme-id>`  
2. Place assets in `themes/<theme-id>/`  
3. Update `themebotpark.json` to reference the new theme.  

---

## Bot Modules & Integrations

- **Dialogue Module**  
  - Supports stateful conversations, slot-filling, and fallback strategies.  
  - Extendable with custom NLP hooks (e.g., Rasa, Dialogflow).

- **Persona Module**  
  - Defines voice parameters, TTS providers, and avatar animations.  
  - Plug in external AI voices (Azure, AWS Polly).

- **Action Module**  
  - Webhooks, REST calls, database queries (MongoDB, PostgreSQL).  
  - IoT triggers via MQTT topics.

- **Analytics Module**  
  - Emits Prometheus metrics.  
  - Custom events logged to Grafana dashboards.

---

## CLI & Workflow

| Command                 | Description                                        |
|-------------------------|----------------------------------------------------|
| `themebotpark init`     | Initialize project, create config skeleton.        |
| `themebotpark scaffold` | Generate themes, bots, channel adapters.           |
| `themebotpark run`      | Launch local dev environment with hot reload.      |
| `themebotpark deploy`   | Deploy to target environment (Docker/K8s).         |
| `themebotpark logs`     | Stream logs from orchestrator and adapters.        |

Typical workflow:  
1. `init` → `scaffold theme` → `scaffold bot` → customize assets & dialogue → `run` to test → `deploy`

---

## Testing & CI/CD

- **Unit Tests**: `npm test` (Jest)  
- **Integration Tests**: `npm run test:integration` (Cypress against local Docker)  
- **Linting**: ESLint + Prettier (`npm run lint`)  
- **GitHub Actions**:  
  - On PR: run lint, unit tests  
  - On merge: build Docker image, push to registry, deploy to staging K8s  

---

## Roadmap

### Phase 1 – MVP

- Core CLI & Orchestrator  
- Slack + Web Widget adapters  
- JSON config schema & validator  
- Basic dialogue & persona modules  
- Local Docker workflow  

### Phase 2 – Expansion

- Discord, Teams adapters  
- Voice assistant integration  
- IoT environment control hooks  
- Theme Registry service  
- Analytics dashboard  

### Phase 3 – Ecosystem

- Theme marketplace  
- Community-contributed templates  
- Visual theme designer UI  
- Enterprise-grade security & multi-tenant support  

---

## Contributing

We welcome all contributions!

1. Fork the repo and create a feature branch.  
2. Follow our [Code Style Guide](CONTRIBUTING.md).  
3. Write unit & integration tests for new features.  
4. Submit a pull request with a clear description of changes.  

Please see [CONTRIBUTING.md](./CONTRIBUTING.md) for full guidelines, issue templates, and code of conduct.

---

## License & Code of Conduct

ThemeBotPark is released under the MIT License.  

Please respect our [Code of Conduct](CODE_OF_CONDUCT.md) to maintain a welcoming community.

---

*End of README*
