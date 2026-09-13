# PSV Sizing Calculator - User Guide

## Quick Start

### Step 1: Open the Calculator
- Open `frontend/index.html` in your web browser
- No installation required for standalone use

### Step 2: Select Your Fluid Type
Choose one of three options:
- **Steam** - For steam relief systems
- **Liquid Hydrocarbon** - For liquid crude, condensate, etc.
- **Gas** - For vapors, crack gas, or any gaseous relief

### Step 3: Enter System Parameters

#### For All Fluids:
```
System Pressure (bar):           [Input your operating/set pressure]
Flow Rate (kg/s):                [Input required relief capacity]
Temperature (°C):                [Input system temperature]
```

#### For Gases (Additional):
```
Fluid Composition (Custom):      [Optional: specify mole % of components]
  - Select from pre-loaded: Crack Gas (Olefin)
  - Or input custom composition
```

### Step 4: Choose Relief Scenario

**Three scenarios available:**

1. **Normal Overpressure**
   - Use for: Pump shutoff, thermal expansion, instrument error
   - Typical overpressure: 10% of set pressure
   - Lowest relief capacity needed

2. **Emergency Relief**
   - Use for: Equipment failure, furnace trip, loss of cooling
   - For crack gas: ~250 tonne/h generation rate
   - Higher capacity than normal (typically 20-50% more)

3. **Fire Case**
   - Use for: External fire exposure
   - Highest relief capacity requirement
   - Governs final valve selection (worst case)

### Step 5: Set Back Pressure

**Option A: Use Typical Olefin Plant Value**
- Flare system back pressure: ~1.0 bar absolute
- Typical for plants with elevated flare header

**Option B: Custom Back Pressure**
- Input your specific flare system back pressure
- ⚠️ Higher back pressure = lower valve capacity
- Verify with flare line engineer

### Step 6: Run Calculation

Click **"CALCULATE"** button

The calculator will:
1. Validate all inputs
2. Calculate required relief capacity
3. Determine orifice area needed
4. Select API 520 standard valve size
5. Verify capacity with selected orifice
6. Flag any safety warnings

### Step 7: Review Results

**Output includes:**

```
📊 RESULTS SUMMARY
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Scenario:              [Your selected scenario]
Required Capacity:     [kg/s]
Calculated Orifice:    [mm²]

✅ RECOMMENDED VALVE SIZE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
API Orifice:          [Letter: D-V]
Orifice Area:         [mm²]
Actual Capacity:      [kg/s]
Capacity Margin:      [%]

📋 SELECTION CRITERIA
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
✓ Actual capacity ≥ Required capacity
✓ Orifice is standard API 520 size
✓ No sanity check failures
⚠️ [Any warnings]
```

---

## Detailed Workflows

### Workflow 1: Sizing PSV for Normal Operation

**Scenario**: Sizing relief valve for liquid storage tank with pump

```
1. Fluid Type:          Liquid Hydrocarbon
2. Operating Pressure:  20 bar
3. Flow Rate:           10 kg/s (36,000 kg/h)
4. Temperature:         40°C
5. Relief Scenario:     Normal Overpressure
6. Back Pressure:       Typical (1 bar abs)
7. Calculate

→ System calculates:
   - Capacity needed: ~10 kg/s
   - Orifice area: ~250 mm²
   - Recommended: Size F (127.4 mm²) → needs 2 valves
            or Size G (204.2 mm²) → might need 2
            or Size H (324.3 mm²) → single valve works
```

### Workflow 2: Emergency Relief for Crack Gas

**Scenario**: Sizing relief for olefin furnace crack gas recovery vessel

```
1. Fluid Type:          Gas (Crack Gas)
2. Composition:         Use pre-loaded "Crack Gas - Olefin"
   (H₂: 35%, CH₄: 25%, C₂H₆: 15%, C₂H₄: 10%, Others: 15%)
3. System Pressure:     8 bar (typical furnace relief pressure)
4. Temperature:         350°C (hot crack gas)
5. Vessel Volume:       250 tonne/h ÷ density ~10 kg/m³ ≈ 100 m³
6. Relief Scenario:     Emergency (furnace trip)
   - Capacity: 250 tonne/h ÷ 1.5 safety factor ≈ 46.4 kg/s
7. Back Pressure:       Typical olefin flare (~1.5 bar abs)
8. Calculate

→ System calculates:
   - Required capacity: ~46.4 kg/s
   - Orifice area needed: ~2,500 mm²
   - Recommended: Size L (1,354.8 mm²) or Size M (2,201.6 mm²)
            or Size N (3,548.0 mm²) - most conservative
```

### Workflow 3: Fire Case Sizing

**Scenario**: Fire relief sizing for atmospheric drum in unit

```
1. Fluid Type:          Liquid Hydrocarbon
2. Pressure:            1 bar (atmospheric)
3. Temperature:         40°C (normal)
4. Vessel Volume:       100 m³ (assume)
5. Relief Scenario:     Fire Case
6. Back Pressure:       0 bar (discharge to atmosphere)
7. Calculate

→ System calculates:
   - Fire heating rate: 43,500 kJ/m²·h (API 520)
   - Surface area × heating → very high vaporization rate
   - Highest capacity requirement
   - Recommended: Larger valve (Size Q-V range likely)
```

---

## Understanding Valve Orifice Sizes

### API 520 Standard Orifice Series

**Size D to F**: Small relief (pilot-operated, small vessels)
**Size G to K**: Medium relief (most common)
**Size L to R**: Large relief (large vessels, high flow)
**Size T to V**: Very large relief (massive vessels or multiple units combined)

### Selection Logic

1. **Calculate required area** from your parameters
2. **Find smallest standard orifice ≥ calculated area**
3. **Verify capacity** with selected orifice exceeds requirement
4. **Safety margin** built in (typically 10-20%)

---

## Sanity Checks - What They Mean

### ✅ All Checks Pass
- Calculation is physically reasonable
- Result can be used for design
- Safe to proceed to engineering review

### ⚠️ Warnings
- **"Back pressure very high"**: Reduces valve capacity significantly
  → Verify flare line design
  → May need larger orifice or multiple valves

- **"Temperature near fluid limit"**: Close to decomposition/critical point
  → Verify fluid properties validity
  → May need to reconsider operating window

- **"Pressure differential very small"**: Low driving force for relief
  → Check set pressure is correct
  → May need pilot-operated valve

- **"Multiple valves may be needed"**: Single orifice too large
  → Select multiple PSVs in parallel
  → Each sized to handle portion of capacity

### ❌ Errors
- **"Orifice area impossibly large"**: Required capacity > largest API orifice
  → Need multiple valves
  → Review if scenario overly conservative
  → Consider higher relief pressure

- **"Invalid composition"**: Mole fractions don't sum to 100%
  → Correct composition input
  → Recalculate

- **"Physical impossibility detected"**: Pressure ratio wrong direction
  → Check inlet > outlet pressure
  → Review input values

---

## Downloading Results

### Generate Report
Click **"GENERATE REPORT"** button to:
- Export detailed PDF with all calculations
- Include step-by-step formulas
- Show assumptions and sanity checks
- Print-ready for engineering records

### Export Data
- Download as CSV for spreadsheet review
- Import into engineering database
- Archive for compliance/audit trail

---

## Troubleshooting

### "Calculation failed - please check inputs"
**Solution**: Verify all fields are filled:
- Pressure > 0 bar
- Temperature in °C (typical: -50 to 500°C)
- Flow rate > 0 kg/s
- Back pressure < inlet pressure

### "Orifice size too large"
**Causes**:
1. Capacity requirement too high (verify scenario)
2. Back pressure too high (check flare system design)
3. Pressure differential too low (increase set pressure?)

**Solutions**:
- Use multiple valves in parallel
- Review if scenario is overly conservative
- Verify back pressure with flare engineer

### "No standard orifice fits"
**Solution**: Results indicate:
- May need custom orifice (non-standard)
- More likely: need multiple standard valves
- Consult with PSV manufacturer

### Unrealistic Results
**Action**: 
1. Double-check all input values
2. Verify units are correct (bar, kg/s, °C)
3. Run "Sanity Check" tool
4. Review documentation for similar case
5. Contact engineering team

---

## Important Notes

### This is a Design Aid Only
✅ Use for preliminary sizing
✅ Use for comparison between options
✅ Use to understand relief system behavior

❌ DO NOT use as final engineering approval
❌ DO NOT skip professional engineer review
❌ DO NOT ignore all warning flags

### Next Steps After Using Calculator

1. **Document Results**: Save calculator output
2. **Engineering Review**: Have licensed PE review findings
3. **Verify Assumptions**:
   - Confirm fluid composition
   - Verify relief pressures
   - Check back pressure with flare expert
   - Validate thermal/mechanical scenarios
4. **Manufacturer Selection**: 
   - Request quotes from valve suppliers
   - Verify actual orifice areas with manufacturer
   - Get performance curves for selected valve
5. **Final Design**: Incorporate valve selection into P&ID and design specs

---

**Questions or Issues?**
Contact: [Your contact info]
Repository: https://github.com/bimalendubarua2016-create/psv-sizing-calculator
