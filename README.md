# 📰 News Alpha Agent

> **Encapsulated news intelligence as a service for other AI agents.**

Fast, private, actionable — the News Alpha Agent wraps proprietary news analysis into a sellable intelligence service. Other agents pay (via x402) to receive trading signals derived from real-time news. The specific news sources stay private; only the intelligence output is sold.

**→ Faster than Bloomberg. Cheaper than analysts. Available 24/7 to any agent.**

---

## 🌾 CROPS Compliance

| Constraint | How We Meet It |
|------------|---------------|
| **Censorship Resistance** | All trades execute on-chain (Base). No platform can freeze trading strategies. Intelligence is delivered peer-to-peer via x402. |
| **Open Source** | Trading logic and signal evaluation framework is fully open source. News source connectors are pluggable — swap in any source. |
| **Privacy** | News analysis runs in Venice (privacy-preserving AI inference — no logs). Trading strategies are never exposed. Signal consumers see outputs, not inputs. |
| **Security** | stETH treasury pattern: principal untouched, only yield funds trades. Maximum loss = accrued interest. Agent has exit paths independent of our infrastructure. |

---

## 🎯 Design Thinking

### The Problem (Empathize)
- Commodity traders need **speed**: information arbitrage decays in minutes
- Bloomberg terminals cost **$24K/year** — not accessible to independent traders or agents
- AI agents trading on prediction markets have **no reliable, fast news sources**
- News APIs are rate-limited, expensive, and not agent-friendly

### The Insight (Define)
> Information is the most valuable commodity in markets. An agent that processes news faster than humans has a systematic edge.

The edge isn't the news itself — it's the **speed of analysis and execution**. By the time a human reads an article, our agent has already:
1. Parsed the event
2. Assessed market impact
3. Evaluated existing positions
4. Executed the trade

### The Solution (Ideate)

**Encapsulated Intelligence Service:**

```
┌─────────────────────────────────────────────┐
│  News Sources (Private, Pluggable)          │
│  • Source A: Real-time event feeds          │
│  • Source B: Geopolitical analysis          │
│  • Source N: [instantiate later]            │
└──────────────┬──────────────────────────────┘
               ↓
┌─────────────────────────────────────────────┐
│  Analysis Engine (Venice — Private AI)      │
│  • Event classification                     │
│  • Impact scoring (0-100)                   │
│  • Market correlation mapping               │
│  • Confidence interval                      │
│  Output: { signal, confidence, markets[] }  │
└──────────────┬──────────────────────────────┘
               ↓
       ┌───────┴───────┐
       ↓               ↓
 ┌──────────┐   ┌──────────────┐
 │ Self-Trade│   │ Sell to Agents│
 │ (bond.cr) │   │ (x402/OpenServ)│
 │ Build     │   │ Intelligence  │
 │ credit    │   │ as a service  │
 └──────────┘   └──────────────┘
```

### The UX (Prototype)

| Stage | Experience | Emotion |
|-------|-----------|---------|
| **Lead-In** | Agent detects breaking news: "Major port disruption in [region]" | Urgency — clock is ticking |
| **Hero Moment** ✨ | In <30 seconds: News → Impact score 87/100 → Correlated markets identified → Trade executed on-chain → All before human Bloomberg readers even open the article | *Speed is the alpha* |
| **What's Next** | Credit score accumulates on-chain (bond.credit). Other agents see your track record and pay for your signals. Passive income from intelligence sales. | Compound advantage |

---

## 🔗 How It Works

### Intelligence Pipeline

```python
# Simplified pipeline (actual source connectors are private)

class NewsAlphaAgent:
    def __init__(self):
        self.sources = []          # Pluggable news sources
        self.analyzer = VeniceAI() # Privacy-preserving inference
        self.trader = OnChainTrader(network="base")
    
    def add_source(self, source):
        """Instantiate a new news source connector"""
        self.sources.append(source)
    
    async def process_event(self, event):
        """Core pipeline: Event → Analysis → Signal → Trade"""
        # 1. Analyze with private AI (no logs)
        analysis = await self.analyzer.assess(event, privacy=True)
        
        # 2. Generate signal
        signal = {
            "event": event.summary,        # Public: what happened
            "impact_score": analysis.score, # Public: how important (0-100)
            "markets": analysis.markets,    # Public: which markets affected
            "direction": analysis.direction,# Public: buy/sell
            "confidence": analysis.conf,    # Public: how sure (0-1)
            "reasoning": "[PRIVATE]",       # Private: never exposed
            "sources": "[PRIVATE]"          # Private: never exposed
        }
        
        # 3. Self-trade (build credit score)
        if signal["confidence"] > 0.7:
            await self.trader.execute(signal)
        
        # 4. Sell signal to subscribers (x402)
        await self.publish_signal(signal)
        
        return signal
```

### On-Chain Credit Building (bond.credit)

```
Agent trades on GMX/Polymarket
  → Win/loss recorded on-chain
  → ERC-8004 identity accumulates credit score
  → Higher credit = other agents trust your signals more
  → More subscribers = more x402 revenue
  → Compound flywheel
```

### Revenue Streams

| Stream | Mechanism | Revenue |
|--------|-----------|---------|
| **Self-trading** | Agent trades based on own signals | Trading profits |
| **Signal sales** | Other agents pay via x402 per signal | Per-signal fee |
| **Subscription** | Agents subscribe for continuous feed | Monthly yield |
| **Credit reputation** | High bond.credit score | Premium pricing |

### Safety: Yield-Only Trading (stETH Treasury)

```
Deposit: $1,000 stETH (principal locked, never touched)
  ↓
Yield: ~$40/year in staking rewards
  ↓
Trading budget: $40/year max exposure
  ↓
Maximum loss: $40 (the yield, never the principal)
  ↓
Principal: always safe, always withdrawable
```

---

## 📁 Project Structure

```
news-alpha-agent/
├── src/
│   ├── agent.py              # Core agent logic
│   ├── analyzer.py           # Impact analysis (Venice AI)
│   ├── trader.py             # On-chain trade execution
│   └── signal_publisher.py   # x402 signal distribution
├── sources/
│   └── base_source.py        # Abstract source connector (open)
│   └── example_rss.py        # Example: RSS feed connector (open)
├── contracts/
│   └── SignalRegistry.sol    # On-chain signal registry
├── docs/
│   └── architecture.md       # Full architecture doc
├── examples/
│   └── sample_signal.json    # Example signal output
└── README.md                 # This file
```

---

## 🏆 Hackathon Tracks

- **bond.credit** — Agent trading + on-chain credit scoring
- **Autonomous Trading (Base)** — Self-directed trading agent
- **Venice: Private Agents** — Privacy-preserving news analysis
- **stETH Agent Treasury (Lido)** — Yield-only trading safety
- **Zyfai** — Yield-funded AI inference

---

## 🔒 Privacy Design

```
What's PUBLIC:                    What's PRIVATE:
  ✅ Signal output                  ❌ News source identities
  ✅ Impact scores                  ❌ Analysis reasoning
  ✅ Trade history (on-chain)       ❌ Source connectors code
  ✅ Credit score                   ❌ Prompt engineering
  ✅ API interface spec             ❌ Correlation models
```

---

## 📜 License

MIT — Framework and signal format are open source.  
News source connectors and analysis models are proprietary.

---

*Built at The Synthesis Hackathon 2026 by Wu Xi*  
*Agent: News Alpha Agent | Harness: Antigravity (Gemini) | Model: gemini-2.5-pro*
