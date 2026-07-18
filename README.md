# 📊 Trender ReplicaPro ULTIMATE v3.0

> Advanced algorithmic trading indicator for TradingView with automated signal
> detection, risk management, performance tracking, and real-time execution
> dashboard.

---

## 📑 Daftar Isi

- [Ringkasan](#-ringkasan)
- [Fitur Utama](#-fitur-utama)
- [Persyaratan](#-persyaratan)
- [Instalasi](#-instalasi)
- [Panduan Konfigurasi](#-panduan-konfigurasi)
  - [1. Main Settings](#1-main-settings)
  - [2. Session Filter](#2-session-filter)
  - [3. Multi-TF Confirmation](#3-multi-tf-confirmation)
  - [4. Volatility Filter](#4-volatility-filter)
  - [5. Break-Even](#5-break-even)
  - [6. Loss Protection](#6-loss-protection)
  - [7. Risk Management](#7-risk-management)
  - [8. Visual Settings](#8-visual-settings)
  - [9. Dashboard](#9-dashboard)
- [Cara Kerja Strategi](#-cara-kerja-strategi)
- [State Machine & Alur Eksekusi](#-state-machine--alur-eksekusi)
- [Panduan Membaca Dashboard](#-panduan-membaca-dashboard)
- [Panduan Alert](#-panduan-alert)
- [Rekomendasi Konfigurasi per Instrumen](#-rekomendasi-konfigurasi-per-instrumen)
- [Troubleshooting](#-troubleshooting)
- [Limitasi & Disclaimer](#-limitasi--disclaimer)
- [Changelog](#-changelog)

---

## 📝 Ringkasan

**Trender ReplicaPro ULTIMATE v3.0** adalah indikator overlay untuk
TradingView yang menggabungkan strategi scalping berbasis EMA crossover
dengan sistem manajemen risiko lengkap. Indikator ini dirancang untuk:

- **Mendeteksi** sinyal BUY/SELL secara otomatis berdasarkan konfirmasi
  multi-indikator
- **Mengelola** posisi dengan trailing stop, break-even, dan dynamic exit
- **Melindungi** modal dengan risk calculator, loss lockout, dan session filter
- **Menampilkan** dashboard real-time yang mencakup monitoring, statistik,
  dan signal eksekusi yang bisa langsung diikuti

### Spesifikasi Teknis

| Item | Detail |
|------|--------|
| Platform | TradingView |
| Bahasa | Pine Script v6 |
| Tipe | Overlay Indicator |
| Tipe Strategi | Scalping / Short-term Swing |
| Timeframe | M1, M5, M15 (auto-adjust) |
| Instrumen | Forex, Crypto, Gold, Futures, Saham |
| Max Labels | 500 |

---

## ✨ Fitur Utama

### Strategi & Sinyal

| Fitur | Deskripsi |
|-------|-----------|
| EMA Crossover | Fast EMA × Slow EMA sebagai sinyal dasar |
| RSI Confirmation | Entry hanya saat RSI mendukung arah (>50 BUY, <50 SELL) |
| EMA 200 Trend Filter | Konfirmasi tren mayor untuk mengurangi false signal |
| ADX Filter | Hanya entry saat kekuatan tren cukup (ADX > threshold) |
| Multi-TF Confirmation | Entry hanya searah tren timeframe lebih tinggi |
| Session Filter | Batasi trading pada jam likuiditas tinggi |
| Volatility Filter | Hindari entry saat BB Squeeze (volatilitas rendah) |

### Manajemen Risiko

| Fitur | Deskripsi |
|-------|-----------|
| Trailing Stop (ATR-based) | SL mengikuti harga secara otomatis berbasis ATR |
| Dynamic SL Multiplier | RSI > 75 → gunakan TP mult (lebih ketat), else → SL mult |
| Break-Even | SL dipindah ke entry setelah profit X ATR |
| Loss Lockout | Pause trading setelah N kerugian berturut-turut |
| Risk Calculator | Hitung lot size otomatis berdasarkan % risiko akun |
| R:R Ratio | Tampilkan Risk-to-Reward ratio secara real-time |

### Monitoring & Statistik

| Fitur | Deskripsi |
|-------|-----------|
| Dashboard Real-time | 24 baris informasi lengkap |
| Execution Signal | Aksi yang harus diambil (BUY/SELL/HOLD/LOCKED) |
| Performance Statistics | Total trades, win rate, profit factor, max drawdown |
| Konfirmasi Checklist | Status semua filter (EMA, RSI, Trend, ADX) |
| Unrealized P&L | Profit/loss posisi berjalan |
| Candle Coloring | Warna candle sesuai posisi (hijau/merah) |

---

## 📋 Persyaratan

- **TradingView** akun (Free atau berbayar)
- **Browser** modern (Chrome, Firefox, Edge, Safari)
- **Pine Script v6** support (default di TradingView saat ini)
- Tidak memerlukan library eksternal atau unduhan tambahan

---

## 🚀 Instalasi

### Langkah 1: Buka Pine Editor

1. Login ke [TradingView](https://www.tradingview.com)
2. Buka chart instrumen yang diinginkan
3. Klik **"Pine Editor"** di bagian bawah layar

### Langkah 2: Tempel Kode

1. Hapus semua kode default di Pine Editor
2. Copy-paste **seluruh kode** Trender ReplicaPro ULTIMATE v3.0
3. Klik **"Add to Chart"**

### Langkah 3: Konfigurasi

1. Klik ikon **⚙️ (gear/settings)** pada indikator di chart
2. Sesuaikan parameter sesuai kebutuhan (lihat Panduan Konfigurasi)
3. Klik **OK**

### Langkah 4: Setup Alert (Opsional)

1. Klik ikon **🔔 (alarm)** di toolbar TradingView
2. Pilih **"Create Alert"**
3. Pilih kondisi: `Trender ReplicaPro ULTIMATE [v3.0]`
4. Pilih salah satu: OPEN BUY / OPEN SELL / CLOSE BUY / CLOSE SELL
5. Atur notifikasi (email, webhook, SMS, dll.)
6. Klik **Create**

---

## ⚙️ Panduan Konfigurasi

### 1. Main Settings

Parameter utama yang menentukan perilaku strategi.

| Parameter | Default | Range | Deskripsi |
|-----------|---------|-------|-----------|
| Timeframe / Mode | M1 (1 Minute) | M1, M5, M15 | Mode trading — semua parameter otomatis menyesuaikan |
| EMA 200 Trend Filter | ✅ Aktif | On/Off | Entry hanya searah EMA 200 |
| ADX Filter | ✅ Aktif | On/Off | Entry hanya saat tren kuat |
| ADX Length | 14 | 5–50 | Periode perhitungan ADX |
| ADX Threshold | 20.0 | 5–100 | Nilai minimum ADX untuk entry |

#### Auto-Adjust Parameters per Mode

| Parameter | M1 | M5 | M15 |
|-----------|-----|-----|------|
| Fast EMA | 5 | 8 | 12 |
| Slow EMA | 12 | 20 | 26 |
| RSI Length | 7 | 9 | 14 |
| ATR Length | 7 | 10 | 14 |
| SL Multiplier | 1.2 | 1.5 | 2.0 |
| TP Multiplier | 0.6 | 0.8 | 1.0 |

> **Tips:** Mode M1 cocok untuk scalping cepat, M5 untuk balance
> antara frekuensi dan akurasi, M15 untuk swing kecil.

---

### 2. Session Filter

Membatasi trading pada jam-jam tertentu untuk menghindari pasar sepi.

| Parameter | Default | Deskripsi |
|-----------|---------|-----------|
| Aktifkan Session Filter | ❌ Nonaktif | On/Off |
| Trading Session | 0800-1700 | Format HHMM-HHMM (timezone exchange) |

#### Rekomendasi Session

| Pasar | Session Terbaik | Waktu (UTC) |
|-------|----------------|-------------|
| Forex Major | London + NY Overlap | 1300-1700 |
| Forex Full | London Session | 0800-1700 |
| Crypto | 24/7 (tidak perlu filter) | — |
| US Stocks | Market Hours | 1430-2100 |
| Gold (XAU) | London + NY | 0800-1700 |

---

### 3. Multi-TF Confirmation

Mengkonfirmasi arah entry dengan tren di timeframe lebih tinggi.

| Parameter | Default | Deskripsi |
|-----------|---------|-----------|
| Aktifkan HTF Confirmation | ❌ Nonaktif | On/Off |
| Higher Timeframe | 60 (1 Hour) | Timeframe konfirmasi |

#### Mapping HTF yang Disarankan

| Chart TF | HTF yang Disarankan |
|----------|-------------------|
| M1 | M15 atau M30 |
| M5 | M30 atau H1 |
| M15 | H1 atau H4 |

> **Peringatan:** Pastikan HTF lebih tinggi dari chart. Jika HTF sama
> atau lebih rendah, konfirmasi tidak efektif.

---

### 4. Volatility Filter

Menghindari entry saat volatilitas sangat rendah (BB Squeeze).

| Parameter | Default | Range | Deskripsi |
|-----------|---------|-------|-----------|
| Aktifkan Volatility Filter | ✅ Aktif | On/Off | On/Off |
| BB Length | 20 | 10–100 | Periode Bollinger Bands |
| BB Multiplier | 2.0 | 0.5–5.0 | Standar deviation multiplier |
| Min Vol % of Average | 50.0% | 10–100 | BB Width minimum dari rata-rata |

> **Tips:** Jika terlalu banyak sinyal terfilter, kurangi Min Vol % ke 30-40%.
> Jika masih banyak false signal, naikkan ke 60-70%.

---

### 5. Break-Even

Memindahkan Stop Loss ke level entry setelah profit mencapai threshold.

| Parameter | Default | Range | Deskripsi |
|-----------|---------|-------|-----------|
| Aktifkan Break-Even | ✅ Aktif | On/Off | On/Off |
| BE Trigger | 1.0 × ATR | 0.5–10 | Profit minimum (dalam ATR) untuk aktifkan BE |
| BE Offset | 0.1 × ATR | 0.0–5.0 | Jarak SL dari entry (untuk cover spread/komisi) |

#### Cara Kerja

```
1. BUY di harga 1.08500, ATR = 0.00100
2. BE Trigger = 1.0 → aktif saat profit ≥ 0.00100
3. Harga naik ke 1.08620 (profit = 1.2 × ATR) → BE aktif
4. BE Offset = 0.1 → SL dipindah ke 1.08500 + 0.00010 = 1.08510
5. Jika harga turun ke 1.08505 → SL 1.08510 tersentuh → profit kecil
   (bukan loss)
```

---

### 6. Loss Protection

Menghentikan trading sementara setelah kerugian beruntun.

| Parameter | Default | Range | Deskripsi |
|-----------|---------|-------|-----------|
| Aktifkan Loss Lockout | ✅ Aktif | On/Off | On/Off |
| Max Consecutive Losses | 3 | 2–10 | Jumlah loss beruntun sebelum lockout |
| Lockout Duration | 20 bars | 5–200 | Durasi pause dalam satuan bar |

#### Ilustrasi

```
Trade 1: Loss (-1.5%)  → consecLoss = 1/3 ⚠️
Trade 2: Loss (-0.8%)  → consecLoss = 2/3 ⚠️
Trade 3: Loss (-1.2%)  → consecLoss = 3/3 → LOCKED (20 bars)
Bar 1-20: Semua sinyal di-skip
Bar 21:   Lockout habis → trading aktif kembali
```

---

### 7. Risk Management

Menghitung ukuran posisi berdasarkan toleransi risiko.

| Parameter | Default | Range | Deskripsi |
|-----------|---------|-------|-----------|
| Risk per Trade | 1.0% | 0.1–10% | Persentase balance yang dipertaruhkan |
| Account Balance | 10,000 | 100–10M | Saldo akun untuk kalkulasi |
| Tick Value | 1.0 | 0.0001–10000 | Nilai per tick per 1 lot standar |
| Lot Decimal Places | 2 | 0–4 | Presisi pembulatan lot size |

#### Referensi Tick Value

| Instrumen | Tick Size | Tick Value (tipikal) |
|-----------|-----------|---------------------|
| EURUSD (5 digit) | 0.00001 | $1.00 per lot standard |
| GBPUSD (5 digit) | 0.00001 | $1.00 per lot standard |
| USDJPY (3 digit) | 0.001 | ~$6.60 per lot standard |
| XAUUSD | 0.01 | $1.00 per lot standard |
| BTCUSD | bervariasi | sesuai exchange |
| US30 | 1.0 | $1.00 per lot standard |

> **Penting:** Tick Value bervariasi per broker. Cek spesifikasi kontrak
> di broker Anda untuk angka yang tepat.

#### Formula Lot Size

```
Risk Amount     = Account Balance × Risk %
SL Distance     = ATR × SL Multiplier
SL Ticks        = SL Distance / Tick Size
Risk per Cont.  = SL Ticks × Tick Value
Lot Size        = Risk Amount / Risk per Cont.
```

---

### 8. Visual Settings

| Parameter | Default | Deskripsi |
|-----------|---------|-----------|
| Tampilkan Label Chart | ✅ Aktif | Label BUY/SELL/CLOSE di chart |
| Ukuran Font Label | small | tiny / small / normal / large / huge |
| Warnai Candle | ✅ Aktif | Hijau=Long, Merah=Short, Default=Flat |

---

### 9. Dashboard

| Parameter | Default | Deskripsi |
|-----------|---------|-----------|
| Tampilkan Dashboard | ✅ Aktif | Table monitoring di chart |
| Posisi Dashboard | top_right | 6 opsi posisi |
| Ukuran Font Dashboard | small | tiny / small / normal / large / huge |

#### Oposisi Posisi

```
┌─────────────┬─────────────────────────┬──────────────┐
│  top_left   │                         │  top_right   │
├─────────────┤                         ├──────────────┤
│             │       CHART AREA        │              │
│ middle_left │                         │ middle_right │
│             │                         │              │
├─────────────┤                         ├──────────────┤
│ bottom_left │                         │ bottom_right │
└─────────────┴─────────────────────────┴──────────────┘
```

---

## 🧠 Cara Kerja Strategi

### Konsep Dasar

Strategi menggunakan **EMA crossover** (Fast EMA × Slow EMA) sebagai
sinyal dasar entry, yang dikonfirmasi oleh **4 filter** sebelum dieksekusi:

```
                    ┌──────────────────┐
                    │  EMA Crossover   │
                    │  (Sinyal Dasar)  │
                    └────────┬─────────┘
                             │
              ┌──────────────┼──────────────┐
              │              │              │
     ┌────────▼───────┐ ┌───▼────────┐ ┌──▼───────────┐
     │  RSI Filter    │ │ EMA 200    │ │  ADX Filter  │
     │  >50 = Bull    │ │ Trend      │ │  >20 = Kuat  │
     │  <50 = Bear    │ │ Filter     │ │  <20 = Lemah │
     └────────┬───────┘ └───┬────────┘ └──┬───────────┘
              │             │              │
              └──────────────┼──────────────┘
                             │
                    ┌────────▼─────────┐
                    │  Optional Filters│
                    │  • HTF Confirm   │
                    │  • Session       │
                    │  • Volatility    │
                    │  • Loss Lockout  │
                    └────────┬─────────┘
                             │
                         ┌───▼───┐
                         │ ENTRY │
                         └───────┘
```

### Sinyal BUY (Long)

Semua kondisi berikut harus **TRUE**:

1. `ta.crossover(fastEMA, slowEMA)` → Fast memotong Slow dari bawah ke atas
2. `rsi > 50` → Momentum bullish
3. `close > baseEMA` → Harga di atas EMA 200 (jika filter aktif)
4. `adxVal > adxThresh` → Tren cukup kuat (jika ADX aktif)
5. `htfFast > htfSlow` → HTF juga bullish (jika HTF aktif)
6. `inSession` → Jam trading aktif (jika session aktif)
7. `volOK` → Volatilitas cukup (jika vol filter aktif)
8. `not isLocked` → Tidak dalam lockout

### Sinyal SELL (Short)

Semua kondisi berikut harus **TRUE**:

1. `ta.crossunder(fastEMA, slowEMA)` → Fast memotong Slow dari atas ke bawah
2. `rsi < 50` → Momentum bearish
3. `close < baseEMA` → Harga di bawah EMA 200 (jika filter aktif)
4. `adxVal > adxThresh` → Tren cukup kuat (jika ADX aktif)
5. `htfFast < htfSlow` → HTF juga bearish (jika HTF aktif)
6. `inSession` → Jam trading aktif (jika session aktif)
7. `volOK` → Volatilitas cukup (jika vol filter aktif)
8. `not isLocked` → Tidak dalam lockout

### Exit Logic

Exit menggunakan **trailing stop ATR-based** dengan dua mode:

| Kondisi RSI | Multiplier Digunakan | Efek |
|------------|---------------------|------|
| RSI > 75 (overbought, untuk Long) | `tpMult` (0.6 default M1) | Trailing lebih ketat → ambil profit cepat |
| RSI < 25 (oversold, untuk Short) | `tpMult` (0.6 default M1) | Trailing lebih ketat → ambil profit cepat |
| RSI normal | `slMult` (1.2 default M1) | Trailing standar → beri ruang bernapas |

> **Logika:** Saat RSI sudah overbought/oversold, peluang reversal tinggi.
> Trailing stop diperketat menggunakan TP multiplier untuk mengunci profit.

---

## 🔄 State Machine & Alur Eksekusi

Indikator menggunakan **state machine** dengan urutan prioritas:
**EXIT → STATS UPDATE → LOCKOUT CHECK → ENTRY**.

```
┌─────────────────────────────────────────────────────────┐
│                     SETIAP BAR                          │
│                                                         │
│  ┌─────────────────────────────────────────────────┐    │
│  │  STEP A: EXIT CHECK                             │    │
│  │                                                 │    │
│  │  Jika inTrade == 1 (Long):                      │    │
│  │    • Hitung trailing stop baru                  │    │
│  │    • Jika BE aktif → paksa trail ≥ BE level     │    │
│  │    • Jika close < trail → EXIT BUY              │    │
│  │                                                 │    │
│  │  Jika inTrade == -1 (Short):                    │    │
│  │    • Hitung trailing stop baru                  │    │
│  │    • Jika BE aktif → paksa trail ≤ BE level     │    │
│  │    • Jika close > trail → EXIT SELL             │    │
│  └─────────────────────┬───────────────────────────┘    │
│                        │                                │
│  ┌─────────────────────▼───────────────────────────┐    │
│  │  STEP B: STATS UPDATE                           │    │
│  │                                                 │    │
│  │  Jika ada exit:                                 │    │
│  │    • Update totalTrades, winCount, lossCount    │    │
│  │    • Update grossProfit, grossLoss              │    │
│  │    • Update totalPnLPct, maxDDPct               │    │
│  │    • Update consecLoss, lockBarStart            │    │
│  │    • Update bestTrade, worstTrade               │    │
│  └─────────────────────┬───────────────────────────┘    │
│                        │                                │
│  ┌─────────────────────▼───────────────────────────┐    │
│  │  STEP C: LOCKOUT CHECK                          │    │
│  │                                                 │    │
│  │  isLocked = consecLoss >= maxLossLock            │    │
│  │             DAN belum lewat lockBars             │    │
│  └─────────────────────┬───────────────────────────┘    │
│                        │                                │
│  ┌─────────────────────▼───────────────────────────┐    │
│  │  STEP D: ENTRY CHECK                            │    │
│  │                                                 │    │
│  │  canEntry = flat AND !locked AND inSession       │    │
│  │             AND volOK                            │    │
│  │                                                 │    │
│  │  Jika canEntry:                                 │    │
│  │    • BUY  → signalBuy  AND htfBull              │    │
│  │    • SELL → signalSell AND htfBear              │    │
│  └─────────────────────┬───────────────────────────┘    │
│                        │                                │
│  ┌─────────────────────▼───────────────────────────┐    │
│  │  STEP E: UPDATE DISPLAY                         │    │
│  │                                                 │    │
│  │  • Update lastSigTxt (persistent)               │    │
│  │  • Update execAction, execEntry, execSL, execTP │    │
│  └─────────────────────────────────────────────────┘    │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

> **Catatan Penting:** EXIT diproses **sebelum** ENTRY. Artinya jika
> trailing stop tersentuh dan posisi ditutup, entry baru bisa langsung
> terjadi di bar yang sama. Ini memastikan tidak ada gap antara posisi.

---

## 📊 Panduan Membaca Dashboard

Dashboard terdiri dari **4 bagian** dengan **24 baris**:

### BAGIAN 1: MONITORING (Row 0–9)

```
┌──────────────────────────────────────────────┐
│  TRENDER ULTIMATE            │  v3.0         │  ← Row 0: Header
├──────────────────────────────────────────────┤
│  Timeframe      │  M1 | Sess:ACTIVE          │  ← Row 1: TF + Session
│  Position       │  LONG (15 bars)            │  ← Row 2: Posisi + durasi
│  Entry / Trail  │  1.08500 / 1.08320         │  ← Row 3: Entry + trailing
│  Unrealized P&L │  +0.23%                    │  ← Row 4: P&L berjalan
│  RSI / ADX      │  RSI:62.5 | ADX:28.5 OK   │  ← Row 5: Momentum
│  ATR / Trend     │  0.00150 | BULL           │  ← Row 6: Volatilitas
│  HTF / Vol       │  HTF:BULL | Vol:NORMAL    │  ← Row 7: Konfirmasi
│  BE / SL-TP     │  BE:ACTIVE | 1.2 / 0.6    │  ← Row 8: BE status
│  Last Signal     │  BUY                       │  ← Row 9: Sinyal terakhir
└──────────────────────────────────────────────┘
```

| Baris | Apa yang Ditampilkan | Interpretasi |
|-------|---------------------|--------------|
| Timeframe | Mode aktif + status session | Pastikan session sesuai jam trading |
| Position | Arah posisi + durasi dalam bar | LONG/SHORT/FLAT |
| Entry / Trail | Harga entry + trailing stop saat ini | Trail bergerak mengikuti harga |
| Unrealized P&L | Profit/loss posisi berjalan (%) | Hijau=profit, Merah=loss |
| RSI / ADX | Nilai RSI + ADX beserta status | ADX OK=kuat, WEAK=lemah |
| ATR / Trend | Nilai ATR + arah tren EMA 200 | BULL/BEAR/NEUTRAL |
| HTF / Vol | Arah HTF + status volatilitas | LOW=choppy, NORMAL=baik |
| BE / SL-TP | Status break-even + multiplier | WAITING/ACTIVE/OFF |
| Last Signal | Sinyal terakhir yang terjadi | BUY/SELL/CLOSE BUY/CLOSE SELL |

### BAGIAN 2: RISK MANAGEMENT (Row 10–13)

```
┌──────────────────────────────────────────────┐
│  ── RISK MANAGEMENT ──                       │  ← Row 10: Separator
│  Risk / Lots     │  1% $100 | 0.15 lot       │  ← Row 11: Ukuran posisi
│  SL Dist / R:R   │  150 ticks | 1:0.50       │  ← Row 12: SL distance
│  Loss Protection │  OK                        │  ← Row 13: Lockout status
└──────────────────────────────────────────────┘
```

| Baris | Interpretasi |
|-------|--------------|
| Risk / Lots | Persentase risiko + dollar amount + lot size yang disarankan |
| SL Dist / R:R | Jarak SL dalam ticks + Risk-to-Reward ratio |
| Loss Protection | OK = aman, WARN = approaching lockout, LOCKED = paused |

### BAGIAN 3: PERFORMANCE STATS (Row 14–18)

```
┌──────────────────────────────────────────────┐
│  ── PERFORMANCE STATS ──                     │  ← Row 14: Separator
│  Trades / Win%   │  45 trades | 62.2%        │  ← Row 15: Win rate
│  PF / Total PnL  │  PF:1.45 | +12.30%       │  ← Row 16: Profit factor
│  MaxDD / Consec  │  -3.20% | 2 cur (max:4)   │  ← Row 17: Drawdown
│  Best / Worst    │  +2.10% / -1.50%          │  ← Row 18: Ekstrem P&L
└──────────────────────────────────────────────┘
```

| Metrik | Formula | Interpretasi |
|--------|---------|--------------|
| Win Rate | wins / total × 100 | >50% bagus, >60% sangat baik |
| Profit Factor | grossProfit / grossLoss | >1.5 = profitable, >2.0 = excellent |
| Max Drawdown | peak-to-trough cumulative P&L | <10% = aman, >20% = bahaya |
| Consecutive Loss | current / max | Jika max > 5, pertimbangkan kurangi risk% |
| Best / Worst | trade terbaik / terburuk | Perbandingan ekspektasi |

### BAGIAN 4: EKSEKUSI ORDER (Row 19–23)

```
┌──────────────────────────────────────────────┐
│  ── EKSEKUSI ORDER ──                        │  ← Row 19: Separator
│  SIGNAL          │ ██ EKSEKUSI BUY ██        │  ← Row 20: AKSI UTAMA
│  Entry / SL      │  1.08500 / 1.08320        │  ← Row 21: Level entry
│  TP (Ref) / R:R  │  1.08560 | 1:0.50         │  ← Row 22: Target
│  Konfirmasi      │  EMA:Bull | RSI:62.5(B)   │  ← Row 23: Checklist
│                  │  Trend:Bull | ADX:28(OK)  │
└──────────────────────────────────────────────┘
```

| Status SIGNAL | Warna | Aksi Pengguna |
|--------------|-------|---------------|
| `EKSEKUSI BUY` | Hijau terang | Buka posisi LONG di harga entry |
| `EKSEKUSI SELL` | Merah terang | Buka posisi SHORT di harga entry |
| `TUTUP BUY` | Kuning | Tutup posisi Long |
| `TUTUP SELL` | Kuning | Tutup posisi Short |
| `HOLD LONG` | Hijau redup | Pertahankan posisi Long, pantau trailing |
| `HOLD SHORT` | Merah redup | Pertahankan posisi Short, pantau trailing |
| `LOCKED (N bars)` | Oranye | Trading di-pause, tunggu N bar lagi |
| `MENUNGGU SINYAL` | Abu-abu | Belum ada sinyal, bersabar |

---

## 🔔 Panduan Alert

Indikator menyediakan **4 alertcondition** yang bisa dikonfigurasi:

| Alert | Trigger | Pesan |
|-------|---------|-------|
| OPEN BUY | Sinyal BUY terpicu | `[Trender] BUY {{ticker}} {{interval}} @ {{close}}` |
| OPEN SELL | Sinyal SELL terpicu | `[Trender] SELL {{ticker}} {{interval}} @ {{close}}` |
| CLOSE BUY | Trailing stop Long tersentuh | `[Trender] CLOSE BUY {{ticker}} {{interval}} @ {{close}}` |
| CLOSE SELL | Trailing stop Short tersentuh | `[Trender] CLOSE SELL {{ticker}} {{interval}} @ {{close}}` |

### Template Variables

| Variable | Deskripsi | Contoh |
|----------|-----------|--------|
| `{{ticker}}` | Simbol instrumen | EURUSD, BTCUSD |
| `{{interval}}` | Timeframe chart | 1, 5, 15 |
| `{{close}}` | Harga close saat alert | 1.08500 |

### Integrasi Webhook

Untuk integrasi dengan bot trading (Telegram, Discord, auto-execution):

```json
{
  "action": "BUY",
  "ticker": "{{ticker}}",
  "interval": "{{interval}}",
  "price": "{{close}}",
  "time": "{{timenow}}"
}
```

---

## 📈 Rekomendasi Konfigurasi per Instrumen

### Forex Major Pairs

```
Mode:           M5 (5 Minutes)
EMA Filter:     ✅
ADX Filter:     ✅ (Threshold: 20)
HTF:            ✅ (H1)
Session:        ✅ (0800-1700)
Vol Filter:     ✅ (Min Vol: 50%)
Break-Even:     ✅ (Trigger: 1.0 ATR)
Loss Lockout:   ✅ (3 losses, 20 bars)
Risk:           1.0%
Tick Value:     1.0 (EURUSD 5-digit)
```

### Gold (XAUUSD)

```
Mode:           M5 (5 Minutes)
EMA Filter:     ✅
ADX Filter:     ✅ (Threshold: 25)
HTF:            ✅ (H1)
Session:        ✅ (0800-1700)
Vol Filter:     ✅ (Min Vol: 40%)
Break-Even:     ✅ (Trigger: 1.5 ATR)
Loss Lockout:   ✅ (3 losses, 25 bars)
Risk:           0.5%
Tick Value:     1.0
```

### Crypto (BTCUSD)

```
Mode:           M15 (15 Minutes)
EMA Filter:     ✅
ADX Filter:     ✅ (Threshold: 25)
HTF:            ❌ (volatilitas terlalu tinggi)
Session:        ❌ (24/7 market)
Vol Filter:     ✅ (Min Vol: 60%)
Break-Even:     ✅ (Trigger: 1.5 ATR)
Loss Lockout:   ✅ (2 losses, 30 bars)
Risk:           0.5%
Tick Value:     sesuai exchange
```

### Indeks (US30, NAS100)

```
Mode:           M5 (5 Minutes)
EMA Filter:     ✅
ADX Filter:     ✅ (Threshold: 20)
HTF:            ✅ (H1)
Session:        ✅ (1430-2100)
Vol Filter:     ✅ (Min Vol: 50%)
Break-Even:     ✅ (Trigger: 1.0 ATR)
Loss Lockout:   ✅ (3 losses, 20 bars)
Risk:           1.0%
Tick Value:     1.0
```

---

## 🔧 Troubleshooting

### Masalah Umum

| Masalah | Penyebab | Solusi |
|---------|----------|--------|
| Tidak ada sinyal | Terlalu banyak filter aktif | Matikan HTF atau Vol Filter, kurangi ADX threshold |
| Terlalu banyak false signal | Filter terlalu longgar | Aktifkan semua filter, naikkan ADX threshold |
| Lockout terus terpicu | Strategi kurang cocok di kondisi market | Ganti timeframe, naikkan maxLossLock, atau kurangi risk% |
| Lot size menunjukkan N/A | Tick Value salah | Cek spesifikasi kontrak broker, sesuaikan tickValInput |
| Dashboard tidak muncul | Show Dashboard nonaktif | Aktifkan "Tampilkan Dashboard" di settings |
| Label menumpuk | Max labels tercapai | Hal ini normal jika chart sudah banyak history. Tidak mempengaruhi sinyal terbaru |
| Session filter memblokir semua | Timezone salah | Cek timezone exchange di TradingView (bukan timezone lokal) |

### Warning di Pine Editor

| Warning | Kode | Dampak | Solusi |
|---------|------|--------|--------|
| Undeclared identifier | CE10272 | Error compile | Pastikan copy-paste kode lengkap |
| Already defined | CE10095 | Error compile | Hapus duplikat variabel |
| Syntax error continuation | CE10156 | Error compile | Semua ternary harus satu baris |
| Function scope | CW10003 | Warning saja | Sudah diperbaiki di v3.0 |

### Tips Optimasi Backtesting

1. **Gunakan mode M5** untuk balance terbaik antara sinyal dan akurasi
2. **Aktifkan HTF Confirmation** untuk mengurangi noise
3. **Naikkan ADX Threshold** ke 25 jika pasar sering ranging
4. **Kurangi Risk %** ke 0.5% untuk instrumen volatile (crypto, gold)
5. **Naikkan Lockout bars** jika sering mengalami drawdown beruntun

---

## ⚠️ Limitasi & Disclaimer

### Limitasi Teknis

| Limitasi | Detail |
|----------|--------|
| Backtesting | Indikator ini **bukan** strategi backtesting — tidak ada `strategy.*` calls. Gunakan manual backtest atau convert ke strategy script |
| Tick Value manual | `tickValInput` harus diisi manual karena `syminfo.tickvalue` tidak universal di semua simbol/broker |
| Max 500 labels | TradingView membatasi jumlah label — di chart dengan history panjang, label lama akan hilang |
| ATR-based SL/TP | SL dan TP berbasis ATR, bukan level support/resistance. Untuk SnR-based, perlu modifikasi manual |
| Tidak ada position sizing otomatis | Lot size hanya **rekomendasi** — tidak ada auto-execution |

### Disclaimer

> **PERINGATAN:** Indikator ini adalah **alat bantu analisis**, bukan
> jaminan profit. Semua trading melibatkan risiko kerugian modal.
> Performa masa lalu tidak menjamin hasil di masa depan. Selalu:
>
> - Gunakan risk management yang tepat
> - Backtest sebelum menggunakan di akun real
> - Mulai dengan akun demo
> - Jangan pernah meresikokan lebih dari yang Anda mampu untuk kehilangan
> - Konsultasikan dengan penasihat keuangan profesional jika diperlukan
>
> Pengembang tidak bertanggung jawab atas kerugian yang timbul dari
> penggunaan indikator ini.

---

## 📋 Changelog

### v3.0 (Ultimate) — Rilis Terbaru

#### Fitur Baru
- ✅ **Session Filter** — Batasi trading pada jam likuiditas tinggi
- ✅ **Multi-TF Confirmation** — Konfirmasi entry dengan HTF
- ✅ **Volatility Filter (BB Squeeze)** — Filter kondisi choppy
- ✅ **Break-Even Logic** — SL otomatis ke entry setelah profit
- ✅ **Consecutive Loss Lockout** — Pause trading setelah N loss
- ✅ **Risk Management Calculator** — Hitung lot size otomatis
- ✅ **Performance Statistics** — Win rate, PF, drawdown, dll.
- ✅ **Candle State Coloring** — Warna candle sesuai posisi
- ✅ **Execution Signal Dashboard** — Panduan eksekusi order

#### Perbaikan
- ✅ Fix label tumpang tindih (`plotshape` → `label.new`)
- ✅ Fix nama alert inkonsisten (`BlackPika` → `Trender`)
- ✅ Fix `syminfo.tickvalue` (input manual)
- ✅ Fix duplikat variabel (CE10095)
- ✅ Fix line continuation (CE10156)
- ✅ Fix `ta.crossover` scope (CW10003/CW10004)
- ✅ Fix lockout 1-bar delay (stats update sebelum lockout check)

### v2.0

#### Fitur Baru
- ✅ ADX Filter
- ✅ Dashboard monitoring (13 baris)
- ✅ Execution signal
- ✅ Font size & position parameters

#### Perbaikan
- ✅ Fix label overlap
- ✅ Fix alert naming

### v1.0 (Original)

- ✅ EMA Crossover (Fast/Slow)
- ✅ RSI Confirmation
- ✅ EMA 200 Trend Filter
- ✅ ATR-based Trailing Stop
- ✅ Dynamic SL/TP Multiplier
- ✅ Basic alerts

---

## 👨‍💻 Author

**Trender ReplicaPro ULTIMATE v3.0**

Dikembangkan sebagai indikator scalping profesional untuk TradingView.
Kode ditulis dalam Pine Script v6 dengan arsitektur state machine,
multi-layer filtering, dan comprehensive dashboard.

---

*Terakhir diperbarui: Juli 2025*
```

---

## File README

Tinggal **copy-paste** seluruh konten markdown di atas ke file `README.md` di repository Anda. Sudah mencakup:

| Bagian | Konten |
|--------|--------|
| Ringkasan | Spesifikasi teknis, target penggunaan |
| Fitur | 20+ fitur terkategorisasi |
| Instalasi | Step-by-step dengan screenshot reference |
| Konfigurasi | Semua 9 parameter group dengan tabel lengkap |
| Strategi | Flowchart visual + penjelasan BUY/SELL/EXIT |
| State Machine | Diagram alur eksekusi per bar |
| Dashboard | Panduan baca 24 baris + interpretasi |
| Alert | Template + webhook JSON |
| Rekomendasi | Config per instrumen (Forex, Gold, Crypto, Index) |
| Troubleshooting | 7 masalah umum + solusi |
| Disclaimer | Limitasi + peringatan risiko |
| Changelog | v1.0 → v2.0 → v3.0 |
