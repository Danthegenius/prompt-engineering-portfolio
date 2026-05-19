# Trading Signal Analyser — Prompt System

## Use Case
A structured prompt for analysing forex or index price action and generating 
a bias-confirmed trading signal with risk parameters.

Designed for: prop traders, funded account holders, trading educators.

---

## The Prompt

### SYSTEM
```
You are a professional market analyst specialising in technical price action 
and risk management. Your role is to evaluate the provided market data and 
generate a structured trading signal report. You do not speculate beyond the 
data. You flag uncertainty explicitly. You never recommend a trade without a 
defined risk parameter.
```

### USER
```
Instrument: {{INSTRUMENT}}
Timeframe: {{TIMEFRAME}}
Current Price: {{PRICE}}
Recent Structure: {{USER_DESCRIPTION_OF_PRICE_ACTION}}
Key Levels: {{SUPPORT_RESISTANCE}}
Bias (if any): {{DIRECTIONAL_BIAS OR "None"}}

Generate a trading signal report using this format:
1. Market Context Summary (2-3 sentences)
2. Structural Bias (Bullish / Bearish / Neutral + reason)
3. Entry Trigger (what price action confirmation to wait for)
4. Trade Parameters:
   - Entry Zone
   - Stop Loss
   - Take Profit 1 (1:1.5 RR minimum)
   - Take Profit 2 (1:3 RR minimum)
5. Invalidation Condition
6. Confidence Level (Low / Medium / High) + reason
```

---

## Sample Output

**Input given:**
- Instrument: EURUSD | Timeframe: H4 | Price: 1.0842  
- Structure: "Price swept a previous low at 1.0810 and is now showing bullish 
  engulfing candles. Higher highs forming."  
- Key Levels: Resistance at 1.0900, Support at 1.0810

**Output generated:**
```
1. Market Context Summary
EURUSD has completed a liquidity sweep of the prior swing low at 1.0810 on H4,
followed by a structural shift to the upside. Price is currently recovering 
into a short-term demand zone.

2. Structural Bias: BULLISH
Reason: Sweep of sell-side liquidity followed by bullish engulfing + 
break of internal structure (BOS) suggests institutional accumulation.

3. Entry Trigger
Wait for a 15-minute bullish close above 1.0858 (internal resistance) 
with volume expansion.

4. Trade Parameters
- Entry Zone: 1.0855 – 1.0865
- Stop Loss: 1.0805 (below the swept low)
- Take Profit 1: 1.0920 (RR ~1.1:1.7)
- Take Profit 2: 1.0975 (RR ~1:2.5)

5. Invalidation Condition
4H candle closes below 1.0808 invalidates the bullish thesis entirely.

6. Confidence Level: MEDIUM
Reason: Structural case is valid but HTF trend is still bearish. 
Counter-trend trades carry elevated failure rate.
```

---

## Why It's Structured This Way

**System/User split:** Keeps the AI in a defined persona. The system layer locks 
the model's role and constraints. The user layer carries all the variable inputs.

**Templated variables with `{{}}` syntax:** Makes the prompt reusable as a tool 
or API call. Any client can drop in their own instrument and structure.

**Structured output format:** Removes LLM hallucination risk by forcing the model 
into a fixed schema. Clients can parse this programmatically.

**Invalidation condition included:** Most beginner prompts skip this. Including it 
signals professional-level thinking and makes the output actually actionable.
