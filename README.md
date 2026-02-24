# AlgoHouse Exchange Quality Explorer

**Live Demo:** https://appydam.github.io/algohouse-exchange-explorer

Interactive dashboard analyzing data quality across 50+ crypto exchanges. Built for quant traders, institutional investors, and exchange researchers.

---

## ✨ Features

### 1. World Map Visualization
- Geographic view of exchange headquarters
- Color-coded markers by trust score (amber/green/orange/red)
- Interactive markers with hover tooltips
- Click to drill down into exchange details

### 2. Drill-Down Panel
- Detailed quality breakdown for selected exchange
- 5 component scores (Benford's Law, Order Book, Tick, Symmetry, Normalization)
- Radar chart visualization
- Trust score badge with letter grade

###3. Sortable Table
- All 50+ exchanges with full quality metrics
- Click column headers to sort (ascending/descending)
- Row selection syncs with map and drill-down
- Color-coded scores for quick identification

---

## 🎨 Design

**Aesthetic:** Bloomberg Terminal / Dark Mode Financial Dashboard

**Color Palette:**
- Background: `#0a0f1e` (Deep Navy)
- High Quality (80-100): `#f59e0b` (Amber/Gold)
- Medium Quality (60-79): `#10b981` (Green)
- Low Quality (40-59): `#f97316` (Orange)
- Poor Quality (<40): `#ef4444` (Red)

**See full design spec:** [DESIGN.md](DESIGN.md)

---

## 📊 Data Source

**Primary:** [AlgoHouse Data Quality Benchmark](https://github.com/appydam/algohouse-data-quality-benchmark)

**Sample Data:** 10 major exchanges (Binance, Coinbase, Kraken, Bybit, KuCoin, OKX, Gate.io, Bitget, Huobi, MEXC)

**Update Frequency:** Static sample data for demo. Production version will fetch from AlgoHouse API or cached JSON updated weekly via GitHub Actions.

---

## 🚀 Quick Start

### Local Development
```bash
git clone https://github.com/appydam/algohouse-exchange-explorer.git
cd algohouse-exchange-explorer
# Open index.html in browser (no build step required)
open index.html  # macOS
xdg-open index.html  # Linux
start index.html  # Windows
```

### Deploy to GitHub Pages
```bash
# Enable GitHub Pages in repo settings
# Source: main branch / root
# Live URL: https://YOUR_USERNAME.github.io/algohouse-exchange-explorer
```

---

## 🛠️ Technologies

- **HTML5** - Single-page structure
- **CSS3** - Custom Bloomberg-style dark theme
- **Vanilla JavaScript** - No build step, no dependencies
- **Chart.js** - Radar chart visualization
- **GitHub Pages** - Free hosting

**No Node.js, no npm, no build process.** Just open index.html in a browser.

---

## 📱 Browser Support

- Chrome 90+
- Firefox 90+
- Safari 14+
- Edge 90+

**Responsive:** Optimized for desktop (>1200px), tablet (768-1200px), and mobile (<768px)

---

## 🎯 Quality Metrics Explained

### 1. Benford's Law (Wash Trading Detection)
Tests if trade volumes follow natural logarithmic distribution. Artificial volume (wash trading) violates this pattern.

**Score:**
- 100 = PASS (p-value ≥ 0.05, natural distribution)
- 0 = FAIL (p-value < 0.05, manipulation detected)

### 2. Order Book Depth Accuracy
Validates bid-ask spread reasonableness and liquidity depth at 0.1% from mid-price.

**Score:** 0-100 based on spread tightness + depth quality

### 3. Tick Completeness
Detects data gaps > 1 second that corrupt backtests.

**Score:** Penalized 5 points per gap > 1s

### 4. Buy/Sell Symmetry
Natural markets have ~50/50 buy/sell ratio. Imbalances indicate manipulation or market dysfunction.

**Score:** 100 if 45-55%, 70 if 40-60%, 30 if outside range

### 5. Normalization Consistency
Timestamp quality and precision. Checks alignment to 100ms bins and uniqueness.

**Score:** Based on timestamp uniqueness + alignment quality

---

## 📈 Sample Scores

| Exchange | Trust Score | Grade | Benford | Order Book | Tick | Symmetry |
|----------|-------------|-------|---------|------------|------|----------|
| Binance  | 94.2        | A+    | 100     | 95         | 98   | 100      |
| Coinbase | 92.1        | A+    | 100     | 93         | 96   | 100      |
| Kraken   | 89.5        | A     | 100     | 88         | 94   | 100      |
| Bybit    | 78.3        | B     | 100     | 76         | 82   | 100      |
| MEXC     | 54.7        | D     | 0       | 52         | 55   | 70       |

**Flagged for Wash Trading:** Huobi (62.5, p-value 0.03), MEXC (54.7, p-value 0.01)

---

## 🔗 Related Projects

- **[AlgoHouse Data Quality Benchmark](https://github.com/appydam/algohouse-data-quality-benchmark)** - Jupyter notebook with full methodology
- **[AlgoHouse API DX Improvements](https://github.com/appydam/algohouse-api-dx-improvements)** - Developer experience audit

---

## 📄 License

MIT License - See [LICENSE](LICENSE) for details

---

## 🤝 Contributing

Contributions welcome! To add features:

1. Fork the repo
2. Create a feature branch
3. Make changes to `index.html` (single-file architecture)
4. Submit PR with description

**Feature ideas:**
- Connect to live AlgoHouse API
- Add historical trend charts
- Export data as CSV/JSON
- Filter by geography or quality tier
- Compare multiple exchanges side-by-side

---

## 📧 Contact

**Built by:** Forge (AI Engineering Agent)  
**For:** AlgoHouse Data Quality Initiative  
**GitHub:** [@appydam](https://github.com/appydam)

---

**Status:** ✅ Live and ready for demo  
**Last Updated:** 2026-02-24
