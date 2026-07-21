<div align="center">

# ⚡ POLYMARKET WEATHER BOT

**Statistical arbitrage engine for prediction markets**

`by Maykon Sanches`

![Python](https://img.shields.io/badge/Python-3.11+-3776AB?style=flat-square&logo=python&logoColor=white)
![Status](https://img.shields.io/badge/status-active-success?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-lightgrey?style=flat-square)
![Markets](https://img.shields.io/badge/markets-25%2B-orange?style=flat-square)

</div>

---

## 🎯 O que faz

Monitora mercados de temperatura na **Polymarket** e detecta quando a soma dos preços reais de execução de várias faixas cai abaixo de $1.00 → lucro matematicamente garantido, independente do resultado.

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

## ⚙️ Pipeline

```
 Gamma API          CLOB (auth)         WebSocket           Telegram
┌──────────┐       ┌──────────┐       ┌──────────┐       ┌──────────┐
│  varre   │──────▶│  orderbook│──────▶│  tempo   │──────▶│  alerta  │
│ mercados │       │   real    │       │  real    │       │ formatado│
└──────────┘       └──────────┘       └──────────┘       └──────────┘
     │                                                          ▲
     ▼                                                          │
┌──────────┐       ┌──────────┐       ┌──────────┐              │
│  NOAA    │       │  Open-   │       │  filtro  │──────────────┘
│  NBM     │──────▶│  Meteo   │──────▶│  liquidez│
└──────────┘       └──────────┘       └──────────┘
```

## 🚀 Destaques técnicos

| | |
|---|---|
| 📊 **Preço real de execução** | simula compra nível-a-nível no orderbook — não confia no preço de tela |
| 🔐 **CLOB autenticado** | leitura de orderbooks em lote via assinatura da carteira Polygon |
| 🔌 **WebSocket persistente** | heartbeat + reconexão automática, zero polling |
| ⚡ **Threading paralelo** | 25+ mercados em <60s (antes: ~4min sequencial) |
| 🌡️ **Multi-modelo climático** | NBM · ECMWF · Météo-France · CMA · GEM — por região |
| 🛡️ **Filtro anti-ruído** | liquidez real do orderbook, não volume histórico da API |

## 🧰 Stack

`Python` `py-clob-client` `websocket-client` `Telegram Bot API` `NOAA NBM` `Open-Meteo`

## 📁 Estrutura

```
bot.py                 loop principal
telegram_alert.py      alertas formatados
scanner.py             scanner standalone
nbm.py                 cliente NOAA NBM
polymarket.py          integração Polymarket
config.example.py      template de config
```

## ▶️ Rodando

```bash
git clone https://github.com/SEU_USUARIO/polymarket-weather-bot.git
cd polymarket-weather-bot
pip install -r requirements.txt
cp config.example.py config.py   # edite com suas credenciais
python bot.py
```

> `DRY_RUN=True` por padrão — apenas alerta, nunca executa ordens.

---

<div align="center">

### Maykon Sanches
📍 São Paulo, Brasil · 🎓 IA · 🐍 Python · 📈 Trading Systems

`open to AI/ML engineering · quantitative systems · backend roles`

</div>

---

<sub>Projeto educacional sobre arbitragem em mercados de previsão. Não é recomendação de investimento.</sub>
