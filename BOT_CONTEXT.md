BOT_CONTEXT.md — Pintu ka poora system (single source of truth)
> **Naye chat me ye file padh li?** Bas. Tumhe kuch poochna nahi.
> User bolega **"kal ka plan banao"** — neeche §5 me exactly likha hai kya dena hai.
> Last updated: **10-Nov-2026, 19:45 IST**
---
1. WHO
	
Naam	Pintu
Kaam	Team Leader, shipyard — Bahrain (Al Muharraq)
Timezone	Ghar/office Bahrain (UTC+3). Market IST (UTC+5:30) follow karta hai
Device	Mobile-first. Laptop sirf journal (Excel/Sheets) ke liye
Capital	₹10,000 — TESTING phase, real paisa nahi
Style	Options only. Futures reject ("future bahut costly hai")
Pasand	Range/zone trading — "niche buy, upper book". Breakout chase nahi
Nahi chahiye	70–80% win-rate jaise jhoothe claims. Sirf asli number
⏰ SABSE ZAROORI — TIMEZONE
User ke screenshot ka filename = BAHRAIN time. IST = Bahrain + 2:30.
```
screenshot 08:20 (Bahrain)  =  10:50 IST
screenshot 07:00 (Bahrain)  =  09:30 IST   <- market KHULA hai
```
Ye galti 3 baar hui hai. Har screenshot ka time +2 ghante 30 minute karke padho.
Check karne ka tareeka: repo ke `state` commit timestamps IST me hote hain — unse cross-check karo.
---
2. KAISE BAAT KARNI HAI
Hinglish me jawab. Script comments English me.
Honest warnings kabhi soften nahi. Loss hai to loss bolo. Model galat tha to bolo.
Ek message = ek step. Confirm hone tak agla kaam nahi.
File dene ho to `.txt` twin banao (raw `.yml` / `.pine` nahi). Download+upload, copy-paste nahi.
Workflow file ka naam exactly `index.yml` hona chahiye. `.txt` andar rakhne se kuch nahi chalta.
Zones list me nahi — chart par DRAW karke dikhao.
Har signal me E / SL / TP / EXIT chaar cheezein honi chahiye.
Strikes + premium + ₹/lot do. Futures levels nahi.
Auto-filled commit message box chhedne ko mat bolo.
---
3. DAILY ROUTINE (standing requirement — dobara mat poochna)
Har din ye order, bina bole:
Volume Profile — Daily + Weekly + Monthly teeno ek saath
HVN / LVN / VAH / VAL — naam se mark karo
Heavy imbalance zones
Buyer-vs-seller read har zone me
OI alignment (option chain)
Zones DRAW karo — ek hi shared price axis par (price + OI ek chart me)
E / SL / TP / EXIT
ATM/OTM CE/PE me convert — strike + premium + ₹/lot
---
4. MUJHE KYA CHAHIYE (data)
Data	Kaun deta hai
NIFTY / SENSEX spot, candles	✅ Main khud — Yahoo Finance v8 chart API, `^NSEI` / `^BSESN`
Option chain OI	❌ Sirf user — screenshot
Volume Profile	❌ Sirf user — screenshot
NSE site — band hai (tested 10-Nov-2026)
`nseindia.com/api/option-chain-indices` → HTTP 404 (geo/UA block).
`nseindia.com/api/equity-stockIndices` → HTTP 404.
Dobara try karne ka fayda nahi. User se screenshot hi maango.
Screenshot maangte waqt exactly ye bolo
> "NIFTY → Expiry **[date]** select karke OI screen bhejo.
> Chaho to saath me SENSEX → Expiry **[date]**."
Expiry wahi maango jo agla tradeable hai — aaj ki expiry ka chain kal bekaar hai.
User ke screenshots hi uske tools ke OI/VP ka source of truth hain.
---
5. TRIGGER: "kal ka plan banao"
User ye bole to bina poochhe ye banao:
Chain maango — agla expiry, NIFTY pehle, SENSEX end me (§4)
Chain mile to max pain calculate karo (code neeche §10)
PCR crossover strike dhundo — jahan PCR 1.0 ke paas ho = pin
Do sabse badi CALL wall + do sabse badi PUT wall nikalo
Zones draw karo — ek chart, left price, right OI, shared y-axis
Plan do: BUY ZONE / BOOK ZONE / SL / EXIT + strike + premium + ₹/lot
Aakhri line: "Ye plan hai — order nahi. Premium BS estimate hai, ±40%."
Agar chain nahi mila to guess mat karo. Bolo: "chain chahiye, iske bina plan jhooth hoga."
---
6. BOT — kya hai, kahan hai
Repo: `pk3372482-ui/gold-sniper` — PUBLIC (user ka decision, badalna nahi)
Live file: `.github/workflows/index.yml`
Build: 588 lines / 29,023 B / md5 `01e0518942c720f046edea9270325043` (verified 10-Nov 19:38 IST)
Chalta hai: cron-job.org har 2 minute `workflow_dispatch` bhejta hai (24×7)
Duplicate: `gold_sniper.yml` (XAUUSD, purana) — chhedna nahi
Kya karta hai
15-min bars par NIFTY 50 + SENSEX + NASDAQ 100 scan → Telegram alert.
Alert me: E / SL / TP / premium / strike / ₹ per lot.
Market config (`opt` tuple = qty, strike step, OTM offset)
```python
NIFTY 50    opt=(65, 50, 3)     # lot 65, 50-pt strikes, OTM3 = ATM+150
SENSEX      opt=(20, 100, 3)    # lot 20, 100-pt strikes, OTM3 = ATM+300
```
```python
K = int(round(bar['c']/ost)*ost + ootm*ost*side)   # + = OTM
```
🔒 v6 FIX (10-Nov, LIVE) — premium-based SL
Problem: SL/TP index points me the (2.5×ATR ≈ 204 pts). OTM3 option ka delta ~0.35.
Iska matlab 204-point index SL = option par −57% = account par −40%.
Fix: ab jo pehle aaye:
```python
PSL = 0.30   # premium -30% par exit
PTP = 0.60   # premium +60% par exit
```
Impact (09-Nov ke asli trade par): SL 24,728 → 24,842. Loss −₹3,867 → −₹2,047.
TP 25,341 (+211%, wall ke paar) → 25,077 (+60%, wall ke neeche) = realistic.
⚠️ Limitation (chhupana nahi): model IV 11% fix hai. IV crush capture nahi hota.
Asli exit model se thoda pehle/baad ho sakta hai.
✅ v6 — holiday guard
```python
if M.get('sess') and datetime.fromtimestamp(now, IST).date().isoformat() in HOLIDAYS:
    continue
```
10-Nov, 24-Nov, 25-Dec (NSE holidays) par bot chup — stale bar se galat signal nahi.
Source of truth
`/home/user/gold_system/_index_bot_v2_src.py` → regenerate: `python3 _gen_index_v2.py`
Panels: `_patch_otm.py`, `_patch_cal2027.py`, `_patch_psl.py`, `_patch_hol2.py` — sab ALREADY RUN, dobara mat chalao.
---
7. EXPIRY ENGINE
```python
EXPIRY_WD = {'NIFTY 50': 1, 'SENSEX': 3}    # Mon=0 → NIFTY Tue, SENSEX Thu
SUPPORTED_YEARS = {2026, 2027}
IV_OPT = 0.11 ; RATE = 0.065
```
Holiday → pichhla trading day
dte ≤ 1 → agla expiry (theta se bachne ke liye). Bot 0-DTE kabhi nahi leta.
NSE 2026 holidays (hardcoded, 15)
Jan 26 · Mar 3 · Mar 26 · Mar 31 · Apr 3 · Apr 14 · May 1 · May 28 · Jun 26 · Sep 14 · Oct 2 · Oct 20 · Nov 10 · Nov 24 · Dec 25
2027 — ESTIMATE (official list nahi aayi)
Jan 26, Mar 10, Mar 22, Mar 26, Apr 14, Apr 15, Apr 19, May 17, Jun 15, Oct 29
Conflicts: Holi Mar 22 vs Mar 23 · Balipratipada Oct 30 vs Nov 1
Verified calendar (Nov–Dec 2026)
Date	NIFTY	SENSEX
09-Nov Mon	17-Nov (8d) — 09-Nov skip, 0d	12-Nov (3d)
10-Nov Tue	🚫 HOLIDAY	—
11-Nov Wed	17-Nov (6d)	19-Nov (8d)
12-Nov Thu	17-Nov (5d)	19-Nov (7d) — 12-Nov skip
16-Nov Mon	23-Nov (7d)	19-Nov (3d)
17-Nov Tue	23-Nov (6d)	19-Nov (2d)
24-Nov Tue	🚫 HOLIDAY	26-Nov (2d)
25-Dec Fri	29-Dec	🚫 HOLIDAY
---
8. OPTION ECONOMICS — ₹10,000 ka sach
Rule of thumb: safe capital ≈ 6–7 × 1 lot premium.
Strike	NIFTY 1 lot (3d)	WR	PF	SENSEX 1 lot	PF
ATM	₹5,962	41.7%	1.59	₹5,994	1.54
OTM1	₹4,482	41.7%	1.61	₹5,040	1.57
OTM2	₹3,276	36.7%	1.62	₹4,193	1.61
OTM3	₹2,324	35.0%	1.62	₹3,449	1.65
OTM4	₹1,598	35.0%	1.65	₹2,805	1.70
Harsh cost (3% spread, IV −2.5): NIFTY ATM 1.26 / OTM3 1.24 · SENSEX OTM3 1.34 / OTM4 1.37.
Sach: ₹10,000 par NIFTY 1 lot = account ka 68–80%. SL lagne par −15% se −26% account.
7-loss streak ke liye ₹11,072 chahiye. Real paisa is account se mat lagao.
₹1,500 se kam premium par charges 4–5% kha jaate hain — chhodo.
---
9. HARD-WON LESSONS (ye galtiyan dobara mat karo)
⏰ TIMEZONE — user ke screenshots Bahrain time hain. IST = +2:30. 3 baar galti hui.
Expiry-day OTM3 bekaar — 0-DTE par delta ~0, sirf theta. 25,100 CE 09-Nov ki value ₹1.30 thi.
Premium vs index SL — option trade ka SL premium me hona chahiye, index points me nahi.
Expiry-week same-side OI wall = FUEL, resistance nahi. (06-Nov: 24,729 → 25,030.)
Teesre din "max pain" par price pin ho jaata hai — 09-Nov: max pain 24,900, spot 24,901.45. 1 point.
PCR crossover (PCR ≈ 1.0) = pin strike. Uske upar call-heavy (ceiling), neeche put-heavy (floor).
24-Nov (monthly) chain ko near expiry samajhna — 09-Nov ko maine ye galti ki.
SENSEX OTM3 (+300 = 0.37%) bahut door — 11.57 lakh call wall ke andar strike utha leta hai. Known issue, open.
Black-Scholes price estimate hai, quote nahi. Asli P&L broker se hi confirm hoga — 09-Nov: model −₹1,840, broker −₹2,514.
1-min GitHub cron kaam nahi karta — cron-job.org `maxdelay=45` chahiye.
NSE API blocked — retry mat karo.
Gold SELL manually mat karo (purana niyam).
---
10. MAX PAIN + PCR — code
```python
def max_pain(oi):
    # oi = {strike: (call_oi, put_oi)}
    def pain(S):
        t = 0
        for k in oi:
            c, p = oi[k]
            t += max(0, S-k)*c + max(0, k-S)*p
        return t
    lo, hi = min(oi), max(oi)
    return min(((S, pain(S)) for S in range(lo, hi+1, 5)), key=lambda x: x[1])

# PCR by strike -> crossover jahan PCR 1.0 ke sabse paas = pin
pcr = {k: v[1]/v[0] for k, v in oi.items()}
```
Reading rule:
PCR > 2 → put-heavy → floor
PCR ≈ 1.0 → pin strike (max pain aksar yahi hota hai)
PCR < 0.5 → call-heavy → ceiling
---
11. HONEST STATS (jhooth nahi)
	WR	PF
NIFTY spot	51.7%	1.73
SENSEX spot	50.0%	1.49
Option 3d (real)	41.7%	1.59
Option 7d (real)	—	1.16
Option 30d (real)	—	0.55
70–80% WR claim retire ho chuka hai. Max 54.4%. PF 1.6 ka matlab: 10 me se 4 jeet, par jeet badi.
Latency: PF 0–75 min tak flat 1.73. `maxdelay=45` accepted.
---
12. LATEST STATE (10-Nov-2026 19:45 IST)
Market band — 10-Nov NSE holiday. Next session Wed 11-Nov 09:15 IST.
Bot state RESET — NIFTY/SENSEX dono `trade: null`. Kal se fresh signal.
09-Nov ka result: NIFTY 25,100 CE, entry 24,932.60 @ ₹105, exit 24,870 par (~₹81). Loss ≈ −₹2,500 se −₹2,700 (broker ne −₹2,514 / −₹2,709 dikhaya). User flat hai.
Lesson: manual SL 24,870 ne bachaya. Bot ka 24,728 hota to −₹3,867.
v6 live: premium SL/TP + holiday guard. Verified 10-Nov 19:38 IST.
---
13. OPEN ITEMS
SENSEX OTM3 strike bahut door — 81,100 jaise strikes call wall ke andar. Fix sochna hai (shayad SENSEX par OTM2).
17-Nov / 19-Nov chain ka screenshot chahiye — Wed ka plan uske bina nahi banega.
Portable memory — ye file hi wo backup hai. Naye chat me sirf ye file bhejo.
₹10,000 capital — position size structurally galat hai. Real paisa lagane se pehle capital badhana hoga.
---
14. EK LINE ME
> Pintu, Bahrain, shipyard TL. ₹10,000 testing. Options only, range trading.
> Hinglish, honest, zones drawn, E/SL/TP/EXIT, ₹/lot. Screenshots Bahrain time (+2:30).
> NSE blocked — OI screenshot hi maango. Bot: `index.yml`, 588 lines, 2-min cron.
