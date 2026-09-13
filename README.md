# PSV Sizing Calculator for Hydrocarbon Plants

## Overview
A comprehensive web-based **Pressure Safety Valve (PSV) Sizing Calculator** designed for hydrocarbon plants, specifically for olefin crack gas systems. This tool helps engineers calculate optimal PSV orifice sizes, valve selections, and capacities for safety-critical applications.

### Key Features
✅ **Multi-Fluid Support**: Steam, Liquid Hydrocarbons, Gases  
✅ **Custom Composition**: User-defined fluid properties  
✅ **Multiple Scenarios**: Normal overpressure, emergency, fire cases  
✅ **API Standard Sizing**: Orifice sizes D, E, F, G, H, J, K, L, M, N, P, Q, R, T, U, V  
✅ **Flare System Integration**: Typical olefin plant back pressure  
✅ **Step-by-Step Calculations**: Transparent formulas with sanity checks  
✅ **Engineering Reports**: Detailed documentation for review and validation  
✅ **Safety Critical**: Built with redundancy checks and warnings  

---

## Project Structure

```
psv-sizing-calculator/
├── frontend/                      # Web interface
│   ├── index.html                # Main calculator page
│   ├── css/
│   │   └── style.css             # Styling
│   └── js/
│       ├── calculator.js         # Main calculation engine
│       ├── fluid-properties.js   # Fluid property database
│       └── ui-handler.js         # User interface logic
├── backend/                       # Server (optional Node.js)
│   ├── server.js                 # Express server
│   ├── calculations/
│   │   ├── psv-formulas.js       # Core PSV sizing formulas
│   │   ├── capacity-calc.js      # Relief capacity calculations
│   │   └── validation.js         # Sanity checks & validation
│   └── data/
│       ├── api-orifice-sizes.js  # API 520 orifice data
│       └── fluid-database.js     # Fluid properties
├── docs/
│   ├── API-520-REFERENCE.md      # API 520 standard reference
│   ├── TECHNICAL-GUIDE.md        # Technical documentation
│   ├── USER-GUIDE.md             # How to use the calculator
│   └── FORMULAS.md               # All formulas with sources
├── tests/                         # Unit tests
│   └── test-calculations.js      # Test suite
└── package.json                  # Project dependencies
```

---

## Technology Stack

- **Frontend**: HTML5, CSS3, JavaScript (ES6+)
- **Backend**: Node.js + Express (optional)
- **Database**: Local JSON data (no external DB required)
- **Deployment**: Static hosting (GitHub Pages, Vercel, Netlify)

---

## Safety & Validation

⚠️ **CRITICAL SAFETY NOTICE**:
- This calculator is a **DESIGN AID ONLY**, not a final approval tool
- All results must be **validated by licensed engineers**
- Results are subject to **site-specific conditions** and company standards
- Every calculation includes **sanity checks** and documented assumptions

---

## License

MIT License