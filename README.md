<div align="center">

# 👋 Maykon Sanches


Formado em Inteligência Artificial

📍 São Paulo, Brasil

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black)

</div>

---

## 📊 Estatísticas

<div align="center">

![GitHub Stats](https://github-readme-stats.vercel.app/api?username=SEU_USUARIO&show_icons=true&theme=tokyonight&include_all_commits=true&locale=pt-br&hide_border=true)

![Top Langs](https://github-readme-stats.vercel.app/api/top-langs/?username=SEU_USUARIO&theme=tokyonight&layout=compact&custom_title=Tecnologias&langs_count=8&hide_border=true)

</div>

---

## ⚡ Projeto em destaque

<div align="center">

### Polymarket Weather Bot
**Sistema de arbitragem estatística em mercados de previsão climática**

</div>

Bot que monitora, em tempo real, mercados de previsão de temperatura na Polymarket e identifica situações em que a soma dos preços reais de execução de várias faixas de resultado fica abaixo de $1.00 — garantindo lucro independente do desfecho.

```
┌─────────────────────────────────────┐
│   18°C  →  25¢                      │
│   19°C  →  24¢                      │
│   20°C  →  16¢                      │
│   21°C  →  12¢                      │
│   22°C  →   8¢                      │
│   23°C  →   5¢                      │
│   ───────────────                    │
│   SOMA  →  90¢   compre todas →      │
│            paga 90¢, recebe $1       │
└─────────────────────────────────────┘
```

```
 Gamma API          CLOB (auth)         WebSocket           Telegram
┌──────────┐       ┌──────────┐       ┌──────────┐       ┌──────────┐
│  varre   │──────▶│ orderbook│──────▶│  tempo   │──────▶│  alerta  │
│ mercados │       │   real   │       │  real    │       │ formatado│
└──────────┘       └──────────┘       └──────────┘       └──────────┘
     │                                                          ▲
     ▼                                                          │
┌──────────┐       ┌──────────┐       ┌──────────┐              │
│  NOAA    │       │  Open-   │       │  filtro  │──────────────┘
│  NBM     │──────▶│  Meteo   │──────▶│  liquidez│
└──────────┘       └──────────┘       └──────────┘
```

| Feature | Descrição |
|---|---|
| 📊 Preço real de execução | simula compra nível-a-nível no orderbook |
| 🔐 CLOB autenticado | leitura de orderbook real via assinatura da carteira |
| 🔌 WebSocket persistente | heartbeat + reconexão automática |
| ⚡ Threading paralelo | 25+ mercados em menos de 60s |
| 🌡️ Multi-modelo climático | NBM · ECMWF · Météo-France · CMA · GEM |

<div align="center">

**[→ ver repositório completo](https://github.com/SEU_USUARIO/polymarket-weather-bot)**

</div>

