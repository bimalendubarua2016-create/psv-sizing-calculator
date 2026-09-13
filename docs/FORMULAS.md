# PSV Sizing Formulas & Calculations

## Safety Notice
⚠️ All formulas below are based on open-source knowledge and API 520 standards.
⚠️ Every calculation must be validated by licensed engineers before use in production.
⚠️ This is a design aid only - not final approval.

---

## 1. RELIEF CAPACITY CALCULATION

### For Gases and Vapors (API 520, Section 5.3.2)

```
📐 FORMULA: Relief Capacity (Mass Flow Rate)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

W = C * A * K * Kb * Kc * √(K * Z * R * T / M * (P1² - P2²))

Where:
  W   = Mass flow rate (kg/s)
  C   = Coefficient of discharge (typical 0.64-0.75)
  A   = Orifice area (mm²)
  K   = Capacity coefficient (function of P2/P1)
  Kb  = Back pressure coefficient
  Kc  = Combination (capacity) correction factor
  K   = Specific heat ratio (Cp/Cv)
  Z   = Compressibility factor
  R   = Gas constant (287 J/kg·K for air reference)
  T   = Temperature (K)
  M   = Molecular weight (kg/kmol)
  P1  = Inlet pressure (bar abs)
  P2  = Outlet/Back pressure (bar abs)

Source: API 520 Part I, Section 5.3.2
Applicable: Gases, vapors, and steam

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

### For Liquids (API 520, Section 5.2.2)

```
📐 FORMULA: Relief Capacity (Liquid)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

W = 51.0 * C * A * √(P1 - P2) / √ρ

Where:
  W     = Mass flow rate (kg/h)
  C     = Coefficient of discharge (0.61-0.69)
  A     = Orifice area (mm²)
  P1    = Inlet pressure (bar abs)
  P2    = Outlet pressure (bar abs)
  ρ     = Density (kg/m³)
  51.0  = Conversion constant

Source: API 520 Part I, Section 5.2.2
Applicable: Incompressible liquids

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## 2. ORIFICE AREA CALCULATION

```
📐 FORMULA: Required Orifice Area
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

A = W_required / (C * K * Kb * Kc * √(K * Z * R * T / M * (P1² - P2²)))

Where:
  A           = Required orifice area (mm²)
  W_required  = Required relief capacity (kg/s)
  (other terms same as above)

Sanity Check:
  - Area must be positive and realistic (typically 1-10,000 mm²)
  - Area should match API 520 standard sizes
  - Result should increase with relief capacity
  - Result should decrease with higher pressure differential

Source: API 520 Part I

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## 3. RELIEF CAPACITY SCENARIOS

### Scenario 1: Normal Overpressure (Pump Shutoff)

```
📐 CALCULATION: Capacity for Normal Overpressure
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

W_normal = Q * ΔP / 100

Where:
  W_normal  = Required capacity (kg/s)
  Q         = Volumetric flow rate (m³/h or equivalent)
  ΔP        = Overpressure allowance (% of set pressure, typically 10%)

Typical values:
  - Pump shutoff: 10% overpressure
  - Thermal expansion: 5-10% overpressure
  - Instrument error: 3-5%

Source: API 520, ASME Section VIII

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

### Scenario 2: Emergency Relief (Furnace Trip)

```
📐 CALCULATION: Capacity for Emergency Conditions
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

W_emergency = (Mass generation rate) / Overpressure limit

For olefin crack gas in furnace trip:
  W_emergency ≈ 250 tonne/h ÷ (1.5 safety factor)
              ≈ 167 tonne/h or ~46.4 kg/s

Note: Emergency relief must handle rapid pressure rise
      Typically requires 20-50% higher capacity than normal

Source: Plant design standards, ASME Section VIII

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

### Scenario 3: Fire Case (External Heat)

```
📐 CALCULATION: Capacity for Fire Exposure
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

W_fire = √(LV * M / (T * Z))

Where:
  L = Heat absorption rate (typically 43,500 kJ/m²·h for fire)
  V = Vessel volume (m³)
  M = Molecular weight (kg/kmol)
  T = Temperature (K)
  Z = Compressibility factor

API 520 Simplified:
  W_fire = 43,500 * L * V / (T * Cp * M)

Where L = Vessel surface area (m²)
      Cp = Heat capacity (kJ/kg·K)

Note: Fire case typically requires highest capacity
      Often 30-100% higher than normal relief

Source: API 520 Part I, Section 3

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## 4. BACK PRESSURE CORRECTION (Kb)

```
📐 FORMULA: Back Pressure Coefficient
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

For non-balanced PSV with back pressure:

Kb = √(1 - Pb/P1)

Where:
  Kb  = Back pressure coefficient (0 to 1)
  Pb  = Back pressure (bar abs)
  P1  = Set pressure (bar abs)

Typical Olefin Plant Flare Back Pressure:
  - Flare system back pressure: 0.5-2.0 bar abs
  - Typical value: ~1.0 bar abs (assuming flare at atmospheric + piping loss)
  - For 10 bar relief: Kb = √(1 - 1/10) = √0.9 ≈ 0.949

⚠️ WARNING: Kb < 1 reduces valve capacity
           Higher back pressure = lower relief capacity
           Must verify flare line design for assumed back pressure

Source: API 520 Part I, Section 5.4

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## 5. API 520 STANDARD ORIFICE SIZES

```
📊 TABLE: API 520 Standard Orifice Areas
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Orifice    Area (mm²)    Area (in²)
─────────────────────────────────
  D         49.2          0.076
  E         78.2          0.121
  F        127.4          0.197
  G        204.2          0.316
  H        324.3          0.502
  J        524.5          0.812
  K        849.0          1.315
  L      1,354.8          2.100
  M      2,201.6          3.410
  N      3,548.0          5.500
  P      5,806.0          9.000
  Q      9,354.3         14.500
  R     14,968.6         23.200
  T     23,548.0         36.500
  U     38,419.2         59.500
  V     62,100.0         96.200

Source: API 520 Part I, Table 8
Note: Areas are nominal, exact values verified from manufacturer specs

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## 6. SANITY CHECKS

```
✅ VALIDATION CHECKS FOR EVERY CALCULATION
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. Orifice Area Reality Check:
   ✓ A must be positive (A > 0)
   ✓ A must be within API 520 range (49-62,100 mm²)
   ✓ A should match standard orifice size
   ✗ If A < smallest orifice: relief capacity too low (impossible)
   ✗ If A > largest orifice: require multiple valves

2. Pressure Differential Check:
   ✓ P1 > P2 (inlet > outlet pressure)
   ✓ ΔP = P1 - P2 should be significant for flow
   ✗ If P1 = P2: no flow possible
   ✗ If P1 < P2: calculation error

3. Temperature Check:
   ✓ Temperature must be in Kelvin (T > 0)
   ✓ Temperature should be realistic for fluid type
   ✗ If T < 0: conversion error
   ✗ If T > fluid decomposition temp: warning

4. Molecular Weight Check (for gases):
   ✓ M > 0 (must be positive)
   ✓ M should match fluid type:
     - Steam: 18
     - Crack gas: 20-30 (mixed composition)
   ✗ If M < 1 or M > 200: likely input error

5. Capacity Check:
   ✓ W should be positive (W > 0)
   ✓ W should increase with relief area
   ✓ W should increase with pressure differential
   ✗ If W decreases with higher ΔP: formula error
   ✗ If W = 0: impossible condition

6. Coefficient Check:
   ✓ C (discharge) = 0.61-0.75 for most PSVs
   ✓ K (compressibility) = 0.7-1.0 for gases
   ✓ Kb (back pressure) = 0-1.0
   ✗ Any coefficient < 0 or > 1.5: error flag

7. Consistency Check:
   ✓ Results for Emergency > Normal relief
   ✓ Results for Fire case ≥ Emergency
   ✗ If not ordered: recalculate or flag warning

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## 7. FLUID PROPERTIES

### Steam
```
PropertyValue
─────────────────────────────
Molecular Weight  18 kg/kmol
Cp/Cv (K)         1.30
Compressibility   0.85-0.95 (function of P,T)
Density           Varies with P,T (use steam tables)
```

### Liquid Hydrocarbons (Typical Crude)
```
Density           850 kg/m³ (approximate)
Viscosity         cSt (variable)
Vapor pressure    < 1 bar (cold)
Molecular Wt      200-300 kg/kmol
```

### Crack Gas (Olefin Plants, Mixed)
```
Typical Composition (mole %):
  H₂:     30-40%     (MW=2)
  CH₄:    20-30%     (MW=16)
  C₂H₆:   10-20%     (MW=30)
  C₂H₄:    5-15%     (MW=28)
  C₃H₆:    3-8%      (MW=42)
  Others:  2-5%

Average MW:  20-25 kg/kmol (depends on composition)
K:           1.2-1.4 (for mixed gas)
Z:           0.85-0.95 (high pressure)
Density:     5-15 kg/m³ (at operating pressure)
```

---

## References

1. **API 520-1, 2020** - Sizing, Selection, and Installation of Pressure-Relieving Devices Part I: Sizing and Selection
2. **ASME Section VIII, Division 1** - Rules for Construction of Pressure Vessels
3. **ISO 4126** - Safety devices for protection of pressure equipment — General rules and devices for unfired pressure vessels
4. **NFPA 68** - Standard on Explosion Protection by Deflagration Venting (if applicable)

---

## Calculation Workflow

```
┌─────────────────────────────────────────────┐
│ 1. Input System Parameters                  │
│    (Pressure, Temp, Flow, Fluid Type)       │
└────────────────┬────────────────────────────┘
                 ↓
┌─────────────────────────────────────────────┐
│ 2. Select Fluid Properties                  │
│    (From database or custom input)          │
└────────────────┬────────────────────────────┘
                 ↓
┌─────────────────────────────────────────────┐
│ 3. Choose Relief Scenario                   │
│    (Normal, Emergency, Fire)                │
└────────────────┬────────────────────────────┘
                 ↓
┌─────────────────────────────────────────────┐
│ 4. Calculate Required Capacity              │
│    W = f(scenario, P, T, composition)       │
└────────────────┬────────────────────────────┘
                 ↓
┌─────────────────────────────────────────────┐
│ 5. Run Sanity Checks                        │
│    (Verify all parameters within range)     │
└────────────────┬────────────────────────────┘
                 ↓
┌─────────────────────────────────────────────┐
│ 6. Calculate Required Orifice Area          │
│    A = f(W, C, K, Kb, Kc, fluid props)      │
└────────────────┬────────────────────────────┘
                 ↓
┌─────────────────────────────────────────────┐
│ 7. Select Standard API Orifice Size         │
│    (Find smallest size ≥ calculated area)   │
└────────────────┬────────────────────────────┘
                 ↓
┌─────────────────────────────────────────────┐
│ 8. Verify Valve Capacity with Selected Size │
│    W_actual = f(A_selected, all parameters) │
└────────────────┬────────────────────────────┘
                 ↓
┌─────────────────────────────────────────────┐
│ 9. Final Sanity Check                       │
│    W_actual ≥ W_required (with margin)      │
└────────────────┬────────────────────────────┘
                 ↓
┌─────────────────────────────────────────────┐
│ 10. Generate Engineering Report             │
│     (All calculations, assumptions, risks)  │
└─────────────────────────────────────────────┘
```

---

**Last Updated**: September 2026  
**Status**: ✅ Documentation Complete | ⏳ Code Implementation in Progress
