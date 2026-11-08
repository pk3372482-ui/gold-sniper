# 🤖 BOT_CONTEXT — Padho Pehle (Pintu ka system)

> **Naye chat me yeh file upload karo (ya repo se padhne ko bolo).**
> Isme sab kuch hai — Pintu kaun hai, kya bana hai, **daily routine kya hai**, kya pending hai.
>
> Repo (public hai, main seedha padh sakta hoon):
> **`https://github.com/pk3372482-ui/gold-sniper`**
>
> Naye chat me bas itna likho:
> **"repo pk3372482-ui/gold-sniper se index.yml padho + BOT_CONTEXT.md padho, phir batao hum kahan the"**

---

## 1️⃣ USER — PINTU

| Cheez | Detail |
|---|---|
| **Naam** | **Pintu** |
| Handle | pk3372482-ui |
| Kaam | **Shipyard me Team Leader** — Bahrain |
| Location | Al Muharraq, Bahrain (IST timezone follow karta hai) |
| **Devices** | ✅ **Laptop hai** + mobile. Journal laptop par (Excel / Google Sheets) |
| Market | **NIFTY 50 + SENSEX — OPTIONS ONLY** |
| Futures | ❌ **Nahi karta** — "future bahut costly hai" |
| **Capital** | **₹10,000** |
| Phase | **TESTING** — asli paisa nahi, abhi seekh raha hai |
| Language | **Hinglish me jawab** |
| Broker | INDmoney / MT5 |

### Lot size (CONFIRMED — Pintu ne khud bataya)
```
NIFTY  : 65 per lot
SENSEX : 20 per lot
```

### 1 lot ki keemat — strike ke hisaab se (3-din expiry, NIFTY lot 65)

| Strike | 1 lot cost | WR | PF | Avg loss |
|---|---|---|---|---|
| **ATM** | ₹5,962 | 41.7% | 1.59 | −₹3,335 |
| OTM1 | ₹4,482 | 41.7% | 1.61 | −₹2,776 |
| **OTM2** | ₹3,276 | 36.7% | 1.62 | −₹2,052 |
| **OTM3** | ₹2,324 | 35.0% | 1.62 | −₹1,582 |
| **OTM4** | ₹1,598 | 35.0% | **1.65** | −₹1,182 |

> **OTM sasta bhi hai aur PF kam bhi nahi hota.** Harsh cost (3% spread + IV -2.5) par bhi
> PF 1.23-1.26 rehta hai — ship line ke upar.
> **Isliye ₹10,000 wale account ke liye ATM nahi, OTM2-3 lena chahiye.**

### 💰 MINIMUM CAPITAL — rule
```
Safe capital  ≈  6-7  x  1 lot ki keemat
```

| Capital | Kya possible |
|---|---|
| ₹5,000 | ❌ Kuch nahi — 1 lot bhi theek se nahi |
| **₹10,000** | ✅ **OTM2-4 (₹1,600-3,300/lot) — chal jaayega** (borderline) |
| ₹15,000 | ✅ OTM comfortable |
| ₹25,000 | ✅ ATM possible (₹6,000/lot) |
| ₹40,000+ | ✅ Proper risk management (1 SL < 8%) |

> **⚠️ MAX 1 LOT.** Do lot kabhi nahi.
> **⚠️ Brokerage + charges** (₹40-80 per round trip) chhote premium par 3-5% kha jaate hain —
> isliye ₹1,500 se sasta option mat lena.

---

## 2️⃣ 🔥 PINTU KA DAILY ROUTINE — YEH SABSE ZAROORI HAI

> **Yeh har din ka kaam hai. Naye chat me bhi yahi karna hai. Har baar poochhna nahi.**

### STEP 1 — Data lao
```
NIFTY 50   : spot, latest OI (option chain)
SENSEX     : spot, latest OI
Data source: Pintu ke screenshots (gocharting / INDmoney) = SOURCE OF TRUTH
             + Yahoo API (^NSEI / ^BSESN) = price history
```

### STEP 2 — VOLUME PROFILE — teeno timeframe EK SAATH
```
DAILY   (120 sessions, bin 25)
WEEKLY  (130 weeks,   bin 50)
MONTHLY (2 saal,      bin 100)
```
**Har timeframe ke liye nikaalo:**
- **POC** (Point of Control) = sabse zyada volume wala price
- **VAH** (Value Area High) = 70% volume ka upper edge
- **VAL** (Value Area Low) = 70% volume ka lower edge

### STEP 3 — HVN / LVN mark karo
```
HVN (High Volume Node)  = volume ka pahaad  →  price ko CHUMBAK ki tarah kheenchta hai
                                              →  strong support/resistance
LVN (Low Volume Node)   = volume ka gaddha  →  price yahan se JALDI bhagta hai
                                              →  breakout/breakdown ka rasta
```
**Chart par naam likh ke mark karna hai** — sirf list me nahi.

### STEP 4 — HEAVY IMBALANCE zones dhoondo
```
Buyer vs Seller ka net farak (volume delta)

T  = total volume
m  = average
ZONE tab jab:  T >= 1.15 x m   AND   |net| >= 0.10
Sort karo:     |net| x sqrt(volume)   (sabse bada pehle)
```
**Har zone ke saath likhna hai: BUYER heavy hai ya SELLER heavy.**

### STEP 5 — OI (option chain) analysis
```
Max Pain       = jahan sabse zyada options expire hote hain
PCR            = put/call ratio
Call walls     = upar ka cap (resistance)
Put walls      = neeche ka floor (support)
```
**gocharting sheet me LEFT = CALLS (CE), RIGHT = PUTS (PE)** — verified.

### STEP 6 — DONO KO EK CHART PAR ALIGN KARO ⭐
```
LEFT panel  = mera Volume Profile (POC/VAH/VAL/HVN/LVN/imbalance)
RIGHT panel = Pintu ke OI ka ladder (calls red, puts green)
SHARED price axis — dono ek hi level par
Shared bands = axhspan se highlight karo
```
> **Yeh step skip mat karo.** Pintu ko zones **drawn** chahiye, list nahi.

### STEP 7 — NEXT-DAY PLAN
Har plan me **chaar cheez** print ho:
```
E    = Entry zone  (buy zone / sell zone)
SL   = Stop loss  (points + %)
TP   = Target  (RR 1:2)
EXIT = Kab nikalna hai (time / condition)
```

### STEP 8 — OPTION me convert karo
```
Plan LONG  →  BUY CALL (CE)   ATM strike
Plan SHORT →  BUY PUT  (PE)   ATM strike
Expiry     →  auto (NIFTY Tuesday, SENSEX Thursday)
Lot        →  NIFTY 65, SENSEX 20
```
Bot ye khud karta hai — Telegram par `OPTION MODE` line.

---

### 📌 ROUTINE KE NORMAL RULES

| Rule | Detail |
|---|---|
| Zones **drawn** karo | "zone mar kr show karna" — list nahi |
| Reasoning **logical** ho | Volume profile ka jawab **kyun** bana, woh bhi bolo |
| Buyer-vs-seller read | **Har zone** ke saath |
| Multi-market numbers | SENSEX / NASDAQ ke numbers bhi do, dodge mat karo |
| Screenshots = truth | Pintu ka tool jo dikhaye wahi final (mera calc nahi) |
| Latest/largest screenshot | Woh bade/clear screenshot dobara bhejta hai — wahi use karo |

---

## 3️⃣ PINTU KI STANDING RULES

### Kaam karne ka tarika
- ✅ **Hinglish** me jawab
- ✅ **Ek step per message**, phir confirmation ka intezaar
- ✅ **Download + upload** (copy-paste nahi)
- ✅ File **`.txt` twin** me do, raw `.yml` / `.pine` nahi
- ✅ **Multi-market numbers** do — "depends" mat bolo
- ✅ **Aaj ka actual call** do, sirf "depends" nahi

### Honesty
- ✅ **"Jo asli number aaye wo dikhao"** — chhupana nahi
- ❌ Jhooth PF dikha ke khush mat karo
- ✅ Analysis me bolo: kitna reliable hai, kitna nahi
- ❌ Out-of-sample PF < 1.15 wala kuch ship mat karo
- ✅ Jab backtest aur Pintu ka live number alag ho → **pehle uska number reproduce karo**

### GitHub par
- ❌ **Auto-filled commit message box mat chhedo**
- ❌ `state.json`, `state_index_v2.json` — **kabhi delete mat karo** (bot ki yaaddasht)
- ✅ File rename phone par karna pade to bolo

### Trading
- ❌ **Asli paisa nahi lagana** — testing phase
- ❌ Gold ka SELL manually nahi lena
- ❌ FundingPips 1-Step **reset nahi karna**
- ✅ News se **15 min pehle** nikal jao
- ✅ **Range trading** pasand hai — "niche buy, upper book". Breakout nahi.

---

## 4️⃣ MAIN PROJECT — Live Bot

### Repo
```
https://github.com/pk3372482-ui/gold-sniper     (PUBLIC)
```

### Files jo matter karti hain
```
.github/workflows/index.yml        ← MAIN BOT (564 lines)
.github/workflows/gold_sniper.yml  ← Gold bot (chal raha hai, trade nahi hota)
state_index_v2.json                ← NIFTY/SENSEX trade state  (CHHEDNA NAHI)
state.json                         ← Gold state  (CHHEDNA NAHI)
```

### Trigger
```
cron-job.org  →  har 2 minute  →  workflow_dispatch
```
**GitHub ka apna cron use NAHI ho raha** — cron-job.org se chal raha hai (100% reliable, 10,000+ runs).

---

## 5️⃣ LIVE BOT KI CONFIG

| Setting | NIFTY 50 | SENSEX | NASDAQ 100 |
|---|---|---|---|
| Timeframe | 15m | 15m | 60m |
| EMA fast | 9 | 9 | 9 |
| EMA slow | 50 | 50 | 50 |
| Trend filter | EMA200 | EMA200 | EMA200 |
| Entry | 3-bar pullback ±0.1% | same | same |
| RSI | >50 buy / <50 sell | same | same |
| SL | 3.0 × ATR(14) | 3.0 × ATR | 2.5 × ATR |
| RR | 1:2 | 1:2 | 1:2 |
| Time stop | 25 bars | 25 bars | 40 bars |
| Entry gate | 14:30 IST tak | 14:30 IST | koi nahi |
| Stale limit | 45 min | 45 min | 90 min |
| Lot | **65** | **20** | MNQ/NQ |
| OPTION MODE | ✅ | ✅ | ❌ (US index) |

### OPTION MODE kya karta hai
```
Bot LONG  →  BUY CALL (CE)   ATM strike
Bot SHORT →  BUY PUT  (PE)   ATM strike
```

**Expiry auto-detect:**
```
NIFTY  weekly expiry = har TUESDAY
SENSEX weekly expiry = har THURSDAY
Holiday ho         → pichla TRADING din
0 ya 1 din bache   → AGLA hafta (theta se bachne ke liye)
```

**Holiday source — 3 layer:**
1. 2026 official list (15 dates) — exact
2. 2027 estimate list (10 dates) — **NSE ne official publish nahi kiya**
3. **Auto-detect** — pichle 60 din ke bars se band din khud dhoondhta hai

**Freshness guard:** alert bhejne se pehle live 1m price dekhta hai.
- Price SL ki taraf 50%+ nikal gayi → **alert skip**
- Price TP ke 75% paas → **alert skip**
- Warna `✅ Entry abhi valid · live XXXX` line

---

## 6️⃣ ASLI NUMBERS (backtest, 60 din, 12-Aug → 08-Nov-2026)

### Spot signals
```
60 trades   ·   WR 51.7%   ·   PF 1.73   ·   +16.5R
```

### Option me convert karne par (ATM, lot 65/20)

| Market | Expiry | Perfect | **Real world** | **Harsh** | 1 lot |
|---|---|---|---|---|---|
| NIFTY | **3 din** | 2.13 | **1.59** ✅ | **1.25** ✅ | ₹5,903 |
| NIFTY | 7 din | 2.00 | 1.16 ⚠️ | 0.74 ❌ | ₹8,962 |
| NIFTY | 30 din | 1.88 | 0.55 ❌ | 0.19 ❌ | ₹18,264 |
| SENSEX | **3 din** | 1.96 | **1.54** ✅ | **1.26** ✅ | ₹5,935 |
| SENSEX | 7 din | 1.75 | 1.11 ❌ | 0.75 ❌ | ₹8,930 |

- **Real world** = 1% spread + IV 1.5 point giri
- **Harsh** = 2% spread + IV 3 point giri

> **Sirf 3-din expiry ship line (PF 1.15) ke upar rehti hai.**
> **Asli dushman = IV CRUSH** — market upar jaata hai to call ki IV girti hai.

### Latency test (alert late aaye to?)
```
15 / 45 / 75 min late  →  PF 1.73 (koi asar nahi)
0/60 trades me trade pehle nikal nahi gayi
```
> Bot ka TP 6×ATR (305 pts) door hai — isliye late alert se nuksan nahi.

### SENSEX option ka risk
```
NIFTY  SL par option -57%  →  ₹4,335 risk
SENSEX SL par option -84%  →  ₹6,009 risk   ← zyada khatarnak
```

---

## 7️⃣ PENDING / NEXT STEPS

| # | Kaam | Status |
|---|---|---|
| 1 | **Monday 09-Nov expiry — pehla live alert ka screenshot** | ⏳ Pintu ko karna hai |
| 2 | NSE official **2027 calendar** aaye to holiday list update | ⏳ NSE publish kare |
| 3 | GitHub 60 din inactivity par workflow **auto-disable** → repo active rakhna | ⚠️ yaad dilana |
| 4 | **₹10,000 par 3 lagatar loss = account khatam** — risk chhota rakhna | 📌 discuss pending |
| 5 | Purana open item: **futures OI** ka screenshot (kabhi nahi bheja) | ⏸️ pending |
| 6 | OTM strike test (sasta option, kam capital ke liye) | 💡 idea |

---

## 8️⃣ BAAKI PROJECTS (abhi active nahi, par bane hue hain)

| Project | Result | Status |
|---|---|---|
| **Gold Sniper v3** (XAUUSD 1h) | 474 trades · 43.7% WR · **PF 1.22** · +53.1R | MT5 EA + Pine — **trade nahi hota** |
| **NASDAQ 1h bot** | 497 trades · 43.5% WR · PF 1.18 | live alert chal raha |
| NIFTY VP / OI charts | 3-timeframe volume profile + OI alignment | files workspace me |
| NIFTY indicators (Pine v6) | NiftyZoneSniper, NiftyIntradaySniper v3_VP | TradingView par |

---

## 9️⃣ TECHNICAL NOTES (jo dobara try nahi karni)

### Data source
```
Yahoo Finance chart API  →  kaam karta hai
  ^NSEI   (NIFTY)   15m, max 60 din
  ^BSESN  (SENSEX)  15m, max 60 din
  NQ=F    (NASDAQ)  60m, 6 mahine
  NSE India API      →  403/404, MAT TRY KARO
  NIFTY futures      →  Yahoo par nahi hai
GitHub raw / API     →  kaam karta hai (repo public hai)
```

### Common bugs jo ho chuke
- Black-Scholes me **holding period din me minus karna** — saal (365) me karna padta hai
- `bash` heredoc me nested quotes → `<<'PY'` use karo
- Scripts ko `cd gold_system` ke baad chalana (PYTHONPATH)
- YAML block scalar ka base indent same hona chahiye
- **Pine never compiled** — error line maango, khud assume mat karo

### Analysis ki galtiyan (dobara mat karna)
- ❌ **"OI wall bada hua → bearish"** — GALAT. Expiry week me bada OI wall = **FUEL** (writer buyback). 06-Nov ko main bearish tha, market **+493 points** chala gaya.
- ❌ Expiry chip galat padhna — **highlighted** chip padho, bagal wala nahi
- ❌ 15m bar ka time-at-price ≠ Pintu ka volume profile (uska tool alag hai)
- ❌ Muhurat trading (08-Nov) ka daily bar **volume 0** hota hai — profile se hatao

---

## 🔟 NAYE CHAT ME KAISE SHURU KARNA

Bas itna likho:

> **"BOT_CONTEXT.md padho (ya repo se padho), phir batao hum kahan the."**

### Ya seedha kaam bolo:
- **"aaj ka plan banao"** → main daily routine (Step 1-8) chala dunga
- **"bot ka status check karo"** → GitHub API se verify kar dunga
- **"expiry kab hai"** → calendar se nikal dunga
- **"naya backtest chalao"** → data laa ke kar dunga
- **"alert me kuch add karo"** → index.yml patch karke naya .txt dunga

---

## 1️⃣1️⃣ EK LINE ME SAB

> **Pintu — Bahrain shipyard me team leader, laptop + mobile. ₹10,000 capital. NIFTY/SENSEX OPTIONS only, max 1 lot (NIFTY 65 / SENSEX 20). Daily routine: D/W/M volume profile → HVN/LVN/VAH/VAL mark → heavy imbalance zones → OI se align → zones DRAW karke chart → E/SL/TP/EXIT plan → bot se ATM CE/PE. Bot live hai: GitHub Actions + cron-job.org har 2 min. Abhi testing — asli paisa nahi. Agla kaam: Monday 09-Nov expiry par pehla live alert verify karna.**

---

*Yeh file ~2026-11-08 ko bani. Jab bhi bada change ho, isko update karna.*
