# AlgoHouse Exchange Quality Explorer - Design Specification

**Style:** Bloomberg Terminal / Dark Mode Financial Dashboard  
**Target:** Quant traders, institutional investors, exchange researchers

---

## Color Palette

### Primary Colors
- **Background:** `#0a0f1e` (Deep Navy) - Bloomberg-style dark mode
- **Surface:** `#1a1f2e` (Slightly lighter navy for cards/panels)
- **Border:** `#2a2f3e` (Subtle borders)

### Quality Indicators
- **High Quality (80-100):** `#f59e0b` (Amber/Gold) - Institutional grade
- **Medium Quality (60-79):** `#10b981` (Green) - Acceptable
- **Low Quality (40-59):** `#f97316` (Orange) - Caution
- **Poor Quality (<40):** `#ef4444` (Red) - Avoid

### Text Colors
- **Primary Text:** `#e5e7eb` (Light gray)
- **Secondary Text:** `#9ca3af` (Medium gray)
- **Accent:** `#60a5fa` (Blue for interactive elements)

---

## Layout Structure

```
┌─────────────────────────────────────────────────────────────┐
│ HEADER                                                       │
│ AlgoHouse Exchange Quality Explorer                         │
│ [Last Updated: 2026-02-24] [50 Exchanges Analyzed]          │
└─────────────────────────────────────────────────────────────┘
│                                                               │
│ ┌───────────────────────────┐ ┌──────────────────────────┐  │
│ │                           │ │                          │  │
│ │   WORLD MAP               │ │  SELECTED EXCHANGE       │  │
│ │   (Exchange HQ locations) │ │  DRILL-DOWN PANEL        │  │
│ │   Color-coded by quality  │ │                          │  │
│ │                           │ │  Exchange: Binance       │  │
│ │   🟡 Binance (Singapore)  │ │  Score: 94.2/100 (A+)   │  │
│ │   🟡 Coinbase (USA)       │ │                          │  │
│ │   🔴 MEXC (Seychelles)    │ │  Components:             │  │
│ │                           │ │  - Benford: 100/100      │  │
│ │                           │ │  - Order Book: 95/100    │  │
│ │                           │ │  - Tick: 98/100          │  │
│ └───────────────────────────┘ └──────────────────────────┘  │
│                                                               │
│ ┌─────────────────────────────────────────────────────────┐ │
│ │ SORTABLE TABLE                                           │ │
│ │                                                           │ │
│ │ Exchange ▼ │ Score │ Grade │ Benford │ OB │ Tick │ Sym │ │
│ │──────────────────────────────────────────────────────── │ │
│ │ Binance    │ 94.2  │  A+   │  100    │ 95 │  98  │ 100 │ │
│ │ Coinbase   │ 92.1  │  A+   │  100    │ 93 │  96  │ 100 │ │
│ │ Kraken     │ 89.5  │  A    │  100    │ 88 │  94  │ 100 │ │
│ │ ...                                                      │ │
│ └─────────────────────────────────────────────────────────┘ │
│                                                               │
│ FOOTER                                                        │
│ Data from AlgoHouse API | Built with Chart.js | GitHub Pages │
└─────────────────────────────────────────────────────────────┘
```

---

## Component Specifications

### 1. Header
- **Height:** 80px
- **Background:** `#0a0f1e` with bottom border `#2a2f3e`
- **Title:** "AlgoHouse Exchange Quality Explorer" (32px, bold, `#e5e7eb`)
- **Subtitle:** Last updated timestamp + exchange count (14px, `#9ca3af`)
- **Logo:** AlgoHouse icon (optional, left side)

### 2. World Map Panel
- **Dimensions:** 600px × 400px
- **Library:** Chart.js Geo plugin or simple SVG map
- **Markers:** Circular dots at exchange HQ coordinates
  - Size: 8-12px diameter based on 24h volume
  - Color: Based on trust score (amber/green/orange/red)
  - Hover: Show exchange name + score
- **Click:** Selects exchange, updates drill-down panel
- **Background:** `#1a1f2e` with subtle border

### 3. Drill-Down Panel
- **Dimensions:** 400px × 400px (matches map height)
- **Background:** `#1a1f2e` with border
- **Default State:** "Select an exchange from map or table"
- **Selected State:**
  - Exchange name (24px bold)
  - Trust score with color badge (e.g., "94.2/100 🟡 A+")
  - Component breakdown:
    - Benford's Law: 100/100 ✓
    - Order Book: 95/100 ✓
    - Tick Completeness: 98/100 ✓
    - Buy/Sell Symmetry: 100/100 ✓
    - Normalization: 92/100 ✓
  - Radar chart showing all 5 dimensions
  - Link to exchange details (if available)

### 4. Sortable Table
- **Width:** Full width (1200px container)
- **Columns:**
  1. Exchange (text, sortable, 150px)
  2. Trust Score (number, sortable, default descending, 100px)
  3. Grade (text, 80px)
  4. Benford (number, sortable, 100px)
  5. Order Book (number, sortable, 100px)
  6. Tick (number, sortable, 100px)
  7. Symmetry (number, sortable, 100px)
  8. Normalization (number, sortable, 100px)
- **Row Height:** 48px
- **Hover:** Background `#1a1f2e` → `#2a2f3e`
- **Click:** Select row, update drill-down panel, highlight on map
- **Header:** Sticky, bold, with sort arrows
- **Score Colors:**
  - 80-100: `#f59e0b` (amber)
  - 60-79: `#10b981` (green)
  - 40-59: `#f97316` (orange)
  - 0-39: `#ef4444` (red)

### 5. Footer
- **Height:** 60px
- **Background:** `#0a0f1e`
- **Text:** "Data from AlgoHouse API | Built with Chart.js | GitHub Pages"
- **Links:** GitHub repo, AlgoHouse API docs, Methodology

---

## Interactions

### Hover States
- **Table rows:** Background lightens
- **Map markers:** Enlarge slightly, show tooltip
- **Buttons:** Border glow

### Click Actions
- **Map marker:** Select exchange, update drill-down + highlight table row
- **Table row:** Select exchange, update drill-down + highlight map marker
- **Column headers:** Sort table by that column

### Responsive Behavior
- **Desktop (>1200px):** Side-by-side layout (map + drill-down)
- **Tablet (768-1200px):** Stack map/drill-down vertically
- **Mobile (<768px):** Hide map, focus on table + drill-down

---

## Typography

- **Headings:** Inter, Roboto, or SF Pro (system font)
- **Body:** Mono for numbers (Roboto Mono, Consolas), Sans for text
- **Sizes:**
  - H1: 32px
  - H2: 24px
  - H3: 18px
  - Body: 14px
  - Small: 12px

---

## Data Source

**AlgoHouse API Endpoint:** `https://api.algohouse.com/v1/exchanges`

**Fallback:** Static JSON file (`data/exchanges.json`) updated weekly via GitHub Actions

**Data Structure:**
```json
[
  {
    "id": "binance",
    "name": "Binance",
    "hq_country": "Singapore",
    "hq_coords": [1.3521, 103.8198],
    "trust_score": 94.2,
    "grade": "A+",
    "components": {
      "benford": 100,
      "orderbook": 95,
      "tick": 98,
      "symmetry": 100,
      "normalization": 92
    },
    "volume_24h": 1234567890
  }
]
```

---

## Technologies

- **HTML5** - Single-page structure
- **CSS3** - Custom styles, no frameworks
- **Vanilla JavaScript** - No build step
- **Chart.js** - For radar charts and potential map visualization
- **GitHub Pages** - Hosting (no backend required)

---

## Performance Requirements

- **Load Time:** < 3 seconds on 3G
- **First Paint:** < 1 second
- **Data Update:** Weekly via GitHub Actions
- **Browser Support:** Chrome 90+, Firefox 90+, Safari 14+

---

## Accessibility

- **WCAG 2.1 AA:** Color contrast meets standards
- **Keyboard Navigation:** Tab through interactive elements
- **Screen Readers:** ARIA labels on map markers and table cells
- **Focus States:** Visible focus indicators

---

**Design Version:** 1.0  
**Date:** 2026-02-24  
**Designer:** Forge (AI Engineering Agent)  
**Status:** Ready for implementation
