<div align="center">

# ⚡ POLYMARKET WEATHER BOT
### `[ statistical arbitrage engine // prediction markets ]`

**by Maykon Sanches**

`Python` · `Real-Time Data` · `WebSocket` · `Applied AI/ML` · `Automated Trading Systems`

---

</div>

```
> initializing arbitrage_engine.py
> scanning 25+ global markets...
> computing real execution price via orderbook simulation...
> status: OPERATIONAL
```

## `> overview`

Sistema autônomo que monitora, em tempo real, mercados de previsão de temperatura na **Polymarket** — uma exchange de contratos preditivos baseada em blockchain — e identifica janelas de **arbitragem estatística**: situações em que a soma dos preços reais de execução de um subconjunto de resultados possíveis de um mesmo mercado cai abaixo de $1.00, garantindo retorno positivo independente do desfecho real.

Não é previsão de mercado. É engenharia de dados aplicada a ineficiência de precificação, executada em produção contra uma API financeira real.

```python
# a lógica central, resumida
if sum(preco_real_execucao(faixa) for faixa in combo) < 1.00:
    lucro_garantido = True  # matematicamente, não estatisticamente
```

## `> engineering highlights`

**Simulação de execução real, não preço de tela**
O preço exibido no orderbook não é o preço pago. O sistema percorre o book nível a nível (asks[0], asks[1], ...) simulando a execução real da ordem, calculando o preço médio ponderado exato que seria pago — eliminando a superestimação de lucro por slippage que derruba estratégias ingênuas de arbitragem.

**Integração autenticada com CLOB via chave criptográfica**
Autenticação via assinatura da carteira Polygon (EIP-712) contra o Central Limit Order Book da Polymarket, com leitura de orderbooks em lote (get_order_books) — de centenas de requisições sequenciais para uma única chamada batch por ciclo.

**Conexão persistente em tempo real**
WebSocket com heartbeat automático e resubscrição transparente após reconexão, eliminando dependência de polling.

**Paralelização de I/O**
Varredura de 25+ mercados internacionais via threading concorrente — de ~4 minutos para menos de 60 segundos por ciclo completo.

**Modelagem meteorológica multi-fonte**
Cada mercado resolve contra uma estação METAR específica (não necessariamente o aeroporto principal da cidade — descoberto via engenharia reversa da documentação de resolução da própria exchange). O sistema seleciona dinamicamente o modelo numérico mais preciso por região: NBM (NOAA) para estações americanas, ECMWF, Météo-France, CMA e GEM via Open-Meteo para o resto do mundo.

**Camadas de filtragem contra falsos positivos**
Liquidez mínima calculada a partir do volume real disponível no orderbook (não do volume histórico exposto pela API pública, que gera falsos positivos em mercados com dados obsoletos), soma configurável por faixa de risco, seleção adaptativa de 5 a 8 outcomes por oportunidade.

## `> stack`

```
Runtime         Python 3.11+
Exchange SDK    py-clob-client (Polymarket oficial)
Real-time       websocket-client
HTTP            requests
Alerting        Telegram Bot API
Data sources    NOAA NBM · Open-Meteo · NWS API
```

## `> architecture`

```
bot.py               → loop principal: varredura, seleção, precificação real
telegram_alert.py    → formatação e disparo de alertas estruturados
scanner.py           → scanner standalone (modo read-only)
nbm.py               → cliente do National Blend of Models (NOAA)
polymarket.py        → camada de integração com a API da Polymarket
config.example.py    → template de configuração (sem credenciais)
```

## `> run`

```bash
git clone https://github.com/SEU_USUARIO/polymarket-weather-bot.git
cd polymarket-weather-bot
pip install -r requirements.txt

cp config.example.py config.py
python bot.py
```

Roda em modo DRY_RUN=True por padrão — observação e alerta, zero execução de ordens.

---

<div align="center">

### `> about the author`

**Maykon Sanches** — São Paulo, Brasil
Formação em Inteligência Artificial · Python · Sistemas de trading automatizado · Integração de dados financeiros em tempo real

Experiência prática em ambientes de missão crítica no setor de meios de pagamento (ecossistema Fiserv CliSiTef/SiTef), aplicada aqui à construção de um sistema autônomo de captura de ineficiências em mercados financeiros descentralizados.

`open to opportunities in AI/ML engineering · quantitative systems · backend`

</div>

---

> Projeto para fins educacionais e de estudo de arbitragem em mercados de previsão. Envolve risco financeiro real se operado em modo de execução (DRY_RUN=False). Não constitui recomendação de investimento.
