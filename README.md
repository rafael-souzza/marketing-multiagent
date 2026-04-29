# 📣 Marketing Content Multi-Agent Pipeline

> Sistema multi-agente que pesquisa tendências em tempo real, gera conteúdo otimizado para SEO com voz de marca consistente, solicita aprovação humana quando necessário e publica automaticamente em WordPress, Instagram e LinkedIn.

---

## 🎯 O Problema que Resolve

Criar conteúdo de marketing relevante, consistente e publicado nos momentos certos exige horas de pesquisa, redação e revisão diárias. Este pipeline automatiza todo esse ciclo com múltiplos agentes de IA especializados, mantendo controle humano nos casos que exigem julgamento editorial.

---

## ⚙️ Como Funciona

O workflow roda **automaticamente todo dia às 7h** e segue o pipeline abaixo:

```
⏰ Cron — disparo diário às 7h
    ↓
🔍 Coleta de tendências em 3 fontes simultâneas:
    ├── SerpAPI — Google Trends
    ├── Reddit API — Posts em alta do setor
    └── RSS Feed — Portais especializados
    ↓
🔗 Merge + Deduplicação dos dados coletados
    ↓
🤖 AI Agent Orquestrador (GPT-4o)
    Decide o tema, formato e ângulo do conteúdo
    ↓
    ├── 🔎 Tool: SEO Reviewer (Claude)
    │       Otimiza título, meta description, palavras-chave
    │
    └── 🗣️ Tool: Brand Voice (Claude)
            Garante tom, estilo e consistência da marca
    ↓
🔧 Parse do output do agente
    ↓
🚦 Precisa de revisão humana?
    ├── ✅ Não → Agendador inteligente define melhor horário
    └── 👤 Sim → Slack para aprovação
                  Webhook aguarda decisão
                  ↓
              Aprovado? → Segue para publicação
              Reprovado? → Salvo no backlog de ideias
    ↓
📤 Publicação simultânea:
    ├── WordPress — artigo completo no blog
    ├── Instagram — caption adaptada
    └── LinkedIn — thread otimizada
    ↓
📊 Google Sheets — log de todas as publicações
📱 Slack — relatório final do dia
```

---

## 🧠 Arquitetura Multi-Agente

O sistema usa **3 agentes de IA com papéis distintos**:

| Agente | Modelo | Responsabilidade |
|---|---|---|
| Orquestrador | GPT-4o | Lê as tendências, decide o tema e delega para as ferramentas |
| SEO Reviewer | Claude 3.5 | Otimiza o conteúdo para rankeamento orgânico |
| Brand Voice | Claude 3.5 | Garante consistência de tom e identidade da marca |

O orquestrador chama os agentes especializados como **ferramentas (tools)**, combinando os outputs antes de decidir se o conteúdo segue direto para publicação ou precisa de revisão humana.

---

## 🔁 Human-in-the-Loop

O sistema não é 100% autônomo por design — conteúdo com temas sensíveis, novidades sem fontes verificadas ou scores de confiança baixos são automaticamente encaminhados para aprovação humana via Slack antes de publicar.

Conteúdo reprovado não é descartado: vai para um **backlog de ideias no Google Sheets** para ser reaproveitado futuramente.

---

## 🛠️ Stack Técnica

| Camada | Tecnologia |
|---|---|
| Orquestração | n8n |
| Agente principal | GPT-4o (OpenAI) |
| Agentes especializados | Claude 3.5 Sonnet (Anthropic) |
| Pesquisa de tendências | SerpAPI + Reddit API + RSS |
| Blog | WordPress REST API |
| Redes sociais | Instagram Graph API + LinkedIn API |
| Logs e backlog | Google Sheets |
| Alertas e aprovação | Slack |
| Agendamento | n8n Cron Trigger |

---

## 📦 Estrutura do Repositório

```
📁 marketing-multiagent/
├── marketing_multiagent_n8n.json   # Workflow completo — importar no n8n
└── README.md
```

---

## 🚀 Como Usar

### Pré-requisitos

- n8n instalado (self-hosted ou cloud)
- API Keys: OpenAI, Anthropic, SerpAPI
- Reddit App criado em reddit.com/prefs/apps
- WordPress com REST API habilitada
- Instagram Business Account + Facebook App
- LinkedIn App com permissões de publicação
- Google Sheets API habilitada
- Bot do Slack configurado

### Instalação

1. Importe `marketing_multiagent_n8n.json` no n8n via **Workflows → Import from file**
2. Configure todas as credenciais no painel do n8n
3. Ajuste o RSS Feed para os portais do seu setor
4. Configure o prompt de Brand Voice com as diretrizes da sua marca
5. Ative o workflow — ele rodará automaticamente às 7h todo dia

---

## 👤 Autor

**Rafael Souzza** — AI/ML Engineer & Automation Consultant  
📍 São Paulo, SP  
🔗 [LinkedIn](https://linkedin.com/in/seu-perfil) | [GitHub](https://github.com/seu-usuario)
