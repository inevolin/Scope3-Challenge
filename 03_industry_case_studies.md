# Scope 3 in Practice: Industry Case Studies

## Overview

Abstract complexity becomes concrete when you trace specific supply chains. This section provides deep-dive case studies for four sectors where Scope 3 accounting is particularly challenging: automotive manufacturing, fashion/apparel, commercial banking, and food & agriculture. For each sector, we map the full value chain, identify the dominant emission categories, and explain why the standard approaches fail.

---

## Case Study 1: Automotive OEM

### Value Chain Map

```mermaid
flowchart LR
    subgraph T3["Tier 3+ Raw Materials"]
        Iron["Iron Ore\nMining"]
        Baux["Bauxite →\nAluminum"]
        Lith["Lithium/Cobalt\nMining (EVs)"]
        Petro["Petroleum →\nPlastics"]
    end

    subgraph T2["Tier 2 Processing"]
        Steel["Steel\nSmelting\n~1.8t CO₂/t steel\n(global avg)"]
        AlumF["Aluminum\nSmelting\n~11t CO₂/t Al"]
        Battery["Battery Cell\nManufacturing\n~30-100 kg CO₂/kWh\n(falling rapidly)"]
        Chem["Chemical\nSynthesis"]
    end

    subgraph T1["Tier 1 Component Suppliers"]
        Body["Body\nPanels"]
        Power["Powertrain\nComponents"]
        BattPk["Battery\nPacks"]
        Elec["Electronics\n& Sensors"]
        Int["Interior\nComponents"]
    end

    subgraph OEM["Auto OEM (Reporting Company)"]
        Manuf["Assembly\nPlant\nScope 1+2"]
        Log["Internal\nLogistics"]
    end

    subgraph DS["Downstream"]
        Deal["Dealerships\n& Distribution\nCat 9"]
        Use["Vehicle\nUse Phase\nCat 11\n~85% of total S3"]
        EoL["End of Life\nRecycling\nCat 12"]
    end

    T3 --> T2 --> T1 --> OEM --> DS

    note1["Cat 1 (upstream):\n~10-15% of total footprint"]
    note2["Cat 11 (use phase):\n~75-85% of total footprint"]

    style Use fill:#e03131,color:#fff
    style Battery fill:#ffa94d,color:#000
    style Steel fill:#ffa94d,color:#000
```

### Emissions Profile: Traditional ICE vs. BEV

| Category | Traditional ICE | Battery EV (grid: 2023 avg) | Battery EV (grid: 100% renewable) |
|----------|----------------|---------------------------|----------------------------------|
| Cat 1 (Steel, Al, components) | ~3 tCO₂e | ~3 tCO₂e | ~3 tCO₂e |
| Cat 1 (Battery production) | — | ~5–10 tCO₂e (falling; leading fabs 3–5t) | ~2–4 tCO₂e |
| Cat 11 (Use phase, 200k km) | ~35–45 tCO₂e | ~15–25 tCO₂e | ~2–5 tCO₂e |
| **Total lifetime** | **~40–50 tCO₂e** | **~25–38 tCO₂e** | **~8–12 tCO₂e** |

### The OEM's Scope 3 Accounting Challenges

**Challenge A: Cat 11 Projection Uncertainty**

A major OEM selling 3 million vehicles per year must estimate the lifetime emissions of those vehicles *at the time of sale*. This requires projections of:

- Grid carbon intensity in 40+ countries over 12–15 years
- EV adoption rate within its own fleet
- Driver behavior and annual mileage
- Vehicle retirement patterns

**Actual industry practice:** Most OEMs use IEA's Stated Policies Scenario (STEPS) for grid projections — which assumes modest policy continuation and does not model rapid decarbonization. Using STEPS vs. IEA's Net Zero Scenario can change Cat 11 estimates by **30–50%** for the same vehicle sold today.

**Challenge B: Battery Supply Chain (Tier 3+ Visibility)**

The cobalt supply chain for EV batteries illustrates the multi-tier data problem:

```mermaid
flowchart TD
    Co["Cobalt Mine\n(DRC — ~70% of global supply)\n\nEmission intensity:\nHighly variable\nArtisanal vs industrial mining\n0.5–8 kg CO₂e/kg Co\n= 16x range"]
    Ref["Cobalt Refiner\n(China — ~80% of refining)\n\nEnergy mix: coal-heavy grid\nIntensity: 15–30 kg CO₂e/kg Co\nrefined to battery-grade"]
    Prec["Precursor\nCathode Active Material\n(PCAM)\nChina, South Korea, Japan"]
    Cell["Battery Cell\nManufacturing\n65–100 kg CO₂e/kWh capacity"]
    Pack["Battery Pack\nAssembly (Tier 1)"]
    OEM["Auto OEM"]

    Co --> Ref --> Prec --> Cell --> Pack --> OEM

    note["OEM has supplier data from Tier 1.\nTiers 2–4 are effectively black boxes\nfor 95% of OEMs."]

    style Co fill:#e03131,color:#fff
    style note fill:#fff3bf,color:#000
```

**Challenge C: The SBTi Paradox for OEMs**

An OEM with a 2030 SBTi target must reduce Cat 11 by 67% (1.5°C pathway). But Cat 11 is determined by:
1. The EV share of new vehicle sales (company controls this)
2. The carbon intensity of the electricity customers use to charge EVs (company cannot control this)
3. The pace of fleet turnover (customers decide when to buy new vehicles)

**Illustrative calculation:** If an OEM sells 3M vehicles/year and sets a Cat 11 target requiring 50% reduction by 2030:

- To achieve through EV mix alone: ~70–80% of new sales must be BEV by 2030 (even with significant grid decarbonization assumed)
- Current (2024) industry average: 15–20% BEV share
- The math requires the OEM to nearly quadruple its BEV penetration in 6 years — which depends on consumer adoption, charging infrastructure, grid capacity, and battery material supply chains that are largely outside its control

---

## Case Study 2: Apparel / Fashion Brand

### Value Chain Map

```mermaid
flowchart TD
    subgraph Raw["Raw Materials (Cat 1 Upstream)"]
        Cotton["Cotton Farming\n~5,000 L water/kg\n~2–6 kg CO₂e/kg\nFertilizer = N₂O"]
        Poly["Polyester\n(Fossil-based)\n~5–15 kg CO₂e/kg"]
        Wool["Wool\n~36 kg CO₂e/kg\n(methane from sheep)"]
        Regen["Recycled Fiber\n~1–3 kg CO₂e/kg\n(potential)"]
    end

    subgraph Process["Processing (Cat 1 Upstream)"]
        Spin["Spinning\n& Weaving"]
        Dye["Dyeing\n& Finishing\n(water, chemicals,\nheat-intensive)"]
        Cut["Cut, Make,\nTrim (CMT)\n(labor-intensive\nlow-tech factories)"]
    end

    subgraph Brand["Brand (Reporting Company)"]
        Design["Design &\nProduct Dev"]
        Proc["Procurement\n& QA"]
        Mktg["Marketing &\nBrand"]
    end

    subgraph DS["Downstream"]
        Ship["Ocean/Air Freight\nCat 4, Cat 9"]
        Retail["Retail\n(Own/Franchise)\nCat 13/14"]
        Use["Consumer\nWashing &\nDrying\nCat 11"]
        EoL["Landfill /\nIncineration\nCat 12\n>85% of apparel"]
    end

    Raw --> Process --> Brand --> DS

    note["Brand employs zero manufacturing workers.\nZero direct control of fabric mills or farms.\nEntire physical supply chain = Scope 3."]

    style note fill:#fff3bf,color:#000
    style Dye fill:#ffa94d,color:#000
    style EoL fill:#e03131,color:#fff
```

### The "Disintermediated Brand" Problem

Fast fashion brands like Zara, H&M, and Shein have almost no direct physical operations — they design, market, and retail. Every single step of physical production is in their Scope 3 (Category 1). The brand's entire climate impact is in its supply chain, and that supply chain:

- Spans 50–100+ countries
- Involves thousands of direct suppliers and tens of thousands of indirect ones
- Operates in jurisdictions with no carbon pricing or emissions reporting requirements
- Changes composition significantly each season

**The tier multiplication problem:**

```mermaid
graph TD
    Brand["Brand\n1 entity"] 
    T1["Tier 1 Garment Factories\n~200–500 factories"] 
    T2["Tier 2 Fabric Mills\n~2,000–5,000 mills"]
    T3["Tier 3 Yarn/Fiber Suppliers\n~10,000+ entities"]
    T4["Tier 4 Raw Material\n~50,000+ farms/mines"]

    Brand --> T1 --> T2 --> T3 --> T4

    note["Engagement cost grows\nexponentially by tier.\nTier 4 is effectively\nunreachable for most brands."]
    T4 --> note

    style Brand fill:#339af0,color:#fff
    style note fill:#fff3bf,color:#000
```

### Dyeing and Finishing: The Hidden Hotspot

The dyeing and finishing stage — converting grey fabric to finished textile — is often the largest single-process emission source within apparel manufacturing, yet receives relatively little public attention.

| Process | Emission Driver | Typical Intensity |
|---------|----------------|-------------------|
| Pre-treatment (scouring, bleaching) | Heat + chemicals | 2–5 kg CO₂e/kg fabric |
| Dyeing | Heat (steam, hot water) + dye chemicals | 3–8 kg CO₂e/kg fabric |
| Finishing (coatings, water repellency) | Heat + fluorochemical treatments | 1–3 kg CO₂e/kg fabric |
| Wastewater treatment | Energy for treatment + methane from effluent | 0.5–2 kg CO₂e/kg fabric |

A fabric mill in Bangladesh running on coal-fired grid power has a dyeing intensity ~4–6x higher than an equivalent mill in Portugal with access to EU grid electricity. Yet both supply identical-looking fabric to a brand that uses an average fabric emission factor per kg.

### Consumer Use Phase: The Inconvenient Category 11

For a pair of jeans, the use phase (washing, drying, ironing over a 5-year life) can account for **30–40%** of total lifecycle emissions. A brand has essentially zero ability to change consumer washing behavior at scale. They can:

- Design for lower wash frequency (longer-lasting treatments)
- Label for cold-water washing
- Release consumer campaigns

None of these interventions can be measured and attributed to the brand's Cat 11 reduction. The category exists in the accounts but cannot be meaningfully managed.

---

## Case Study 3: Commercial Bank — Financed Emissions

### Why Banks' Scope 3 Dwarfs Their Other Emissions

```mermaid
flowchart LR
    subgraph Bank["Large Commercial Bank (Illustrative)"]
        Ops["Operational\nEmissions\n(Scope 1+2)\n\n~100,000 tCO₂e/yr\nOffices + data centers"]
        
        Cat15["Financed Emissions\n(Scope 3 Cat 15)\n\n~150–500 MtCO₂e/yr\n= 1,500–5,000x operational\n\nLoan book: $500B+\nSpanning all sectors"]
    end

    style Ops fill:#69db7c,color:#000
    style Cat15 fill:#e03131,color:#fff
```

### The PCAF Attribution Calculation in Practice

A bank with a $500M loan to an oil & gas company:

```
Company enterprise value (equity + net debt) = $20B
Outstanding loan = $500M
Attribution factor = $500M / $20B = 2.5%

Company Scope 1+2+3 emissions = 50 MtCO₂e/year

Bank's attributed financed emissions = 2.5% × 50 MtCO₂e = 1.25 MtCO₂e/year
```

This single loan generates financed emissions equal to **12.5 times** the bank's entire operational footprint.

### The Engagement vs. Divestment Dilemma

```mermaid
flowchart TD
    START["Bank has Net-Zero\ncommitment by 2050"]

    Q1{"Client is high-emitting\nsteel/cement company"}

    Engage["Strategy A: Engage\n\nContinue lending.\nRequire client to develop\ndecarbonization plan.\nMay offer green financing\nat preferential rates.\n\nPro: Enables transition finance.\nCon: Emissions remain attributed\nto bank for duration.\nCon: Client may not deliver."]

    Divest["Strategy B: Divest/Exit\n\nRefuse new loans.\nAllow existing to mature.\nBank's financed emissions drop.\n\nPro: Reduces bank's Cat 15.\nCon: Client finds another lender.\nActual world emissions unchanged.\nCon: 'Carbon leakage' to less\nscrutinized balance sheets."]

    Green["Strategy C: Transition Finance\n\nLend specifically for\ndecarbonization projects:\nGreen steel capex,\nCCS infrastructure,\nElectrification.\n\nPro: Finances real-world change.\nCon: Still attributed as financed\nemissions until project reduces\nclient's Scope 1+2."]

    START --> Q1
    Q1 --> Engage
    Q1 --> Divest
    Q1 --> Green

    Insight["Key Insight: PCAF attribution\nrewards divestment even when\nengagement produces better\nreal-world outcomes.\nThis is a fundamental flaw\nin financed emission accounting."]

    Engage --> Insight
    Divest --> Insight
    Green --> Insight

    style Insight fill:#fff3bf,color:#000
```

### The SME Lending Black Hole

Large corporate clients (Fortune 500) have Scope 1+2+3 disclosures that banks can use for PCAF calculations. But the majority of bank loan books by *count* (though not by value) consists of SME loans — companies with annual revenues of $1M–$50M that have never produced a GHG inventory.

For these loans, PCAF requires the "spend-based fallback" — essentially applying sector-average emission intensities. This produces numbers with **±200–500%** uncertainty, and provides no ability to track improvement over time.

**Illustrative coverage gap:**

| Loan Segment | % of Loan Book by Value | PCAF Data Quality | Confidence |
|-------------|------------------------|------------------|------------|
| Investment-grade corporates | 40% | Primary (Scope 1+2 disclosed) | High |
| Sub-investment-grade corporates | 20% | Secondary (some disclosure) | Medium |
| Mid-market companies | 25% | Mostly spend-based | Low |
| SME / Small Business | 15% | Spend-based fallback | Very Low |

A bank claiming "net-zero financed emissions by 2050" with 40% of its book in the "very low confidence" category is making a claim that is essentially unmeasurable with current data infrastructure.

---

## Case Study 4: Food & Beverage — Agricultural Emissions

### Why Agriculture Is Uniquely Difficult

Agricultural emissions are:
1. **Biogenic** — from living organisms (methane from cattle enteric fermentation, N₂O from fertilizer)
2. **Spatially distributed** — millions of farms across hundreds of geographies
3. **Highly variable** — same crop, different country, 5–10x emission intensity difference
4. **Not covered by most emission factor databases** — agricultural process emissions require specialized models (IPCC Tier 2/3)

```mermaid
flowchart LR
    subgraph Farm["Agricultural Production (Cat 1 - dominant)"]
        Rice["Rice Paddies\nMethane emissions\n~450 kg CO₂e/t rice\n(flooded cultivation)"]
        Cattle["Beef Cattle\nEnteric fermentation\n~25–50 kg CO₂e/kg beef\n(varies 2x by system)"]
        Dairy["Dairy\n~2–4 kg CO₂e/kg milk"]
        Soy["Soybeans\n~0.4–3 kg CO₂e/kg\n(huge deforestation risk)"]
        Coffee["Coffee\n~5–15 kg CO₂e/kg\n(processing + transport)"]
    end

    subgraph LUC["Land Use Change (Cat 1 - potentially catastrophic)"]
        Def["Deforestation\nfor new agricultural\nland\n\nPeat conversion =\n50–100 years of\ncarbon debt"]
    end

    subgraph Proc["Processing & Manufacturing"]
        Mill["Milling,\nBlending,\nPasteurization"]
        Pack["Packaging\n(plastics, glass,\naluminum)"]
    end

    subgraph Brand2["Food Brand"]
        R&D2["R&D +\nMarketing"]
    end

    subgraph DS2["Downstream"]
        Cold["Cold Chain\nLogistics"]
        Retail2["Grocery\nRetail"]
        Cook["Consumer\nCooking\nCat 11"]
        Waste["Food Waste\n(30–50% of\nfood produced)\nCat 12"]
    end

    Farm --> LUC
    Farm --> Proc
    LUC --> Proc
    Proc --> Brand2 --> DS2

    style Def fill:#e03131,color:#fff
    style Cattle fill:#ffa94d,color:#000
```

### The Deforestation Time-Bomb

Land use change (LUC) associated with agricultural expansion — particularly in tropical regions — releases enormous carbon stocks stored in forests, peatlands, and grasslands. A single hectare of tropical peatland drained for palm oil plantation can release **50–200 tCO₂e/year** for decades as the peat oxidizes.

Under current GHG Protocol rules, LUC emissions are allocated to the commodity produced on the land (palm oil, soy, beef). But:

- Attribution requires knowing *when* land was converted (pre- or post-1994 baseline?)
- Attribution requires satellite mapping of deforestation events linked to specific farms
- Most buyers have no visibility into which farms their commodities come from (especially through traders)

```mermaid
flowchart LR
    Farm1["Deforestation\nFarm A\nHigh LUC carbon debt"]
    Farm2["Sustainable\nFarm B\nNo LUC"]
    Farm3["Farm C"]
    Trader["Commodity\nTrader\n\nMixes grain from\nhundreds of farms.\nNo farm-level traceability."]
    Brand3["Food Brand\n\nBuys 'Brazilian soy'\nfrom trader.\nCannot distinguish\nFarm A from Farm B."]

    Farm1 --> Trader
    Farm2 --> Trader
    Farm3 --> Trader
    Trader --> Brand3

    Result3["Result: Brand must use\nnational/regional average\nLUC emission factor.\nCannot reward sustainable\nfarmers vs. deforesters."]
    Brand3 --> Result3

    style Farm1 fill:#e03131,color:#fff
    style Farm2 fill:#2f9e44,color:#fff
    style Result3 fill:#fff3bf,color:#000
```

**Why this matters:** If a food brand sources soy from Brazil, should it use:
- Brazil national average soy LUC factor: ~3–5 kg CO₂e/kg soy
- Amazon biome average: ~8–12 kg CO₂e/kg soy
- Certified deforestation-free: ~0.3–0.8 kg CO₂e/kg soy

The range is **15–40x**. The choice of emission factor has more impact on the reported footprint than any supply chain intervention the brand could make in the near term.

### Food Waste: The Category No One Wants to Own

Approximately **30–40% of all food produced globally is wasted** — in production, transport, retail, and consumption. The emissions associated with producing that wasted food are not formally allocated to any Scope 3 category by most companies. They appear in Cat 12 (end-of-life treatment — methane from landfilled food) but the *upstream production emissions of the food that was wasted* are attributed to the food that was *consumed*.

This is a category-level attribution failure: the system does not capture the full cost of waste, which disincentivizes investment in waste reduction.

---

## Cross-Sector Summary: The Common Failure Patterns

```mermaid
flowchart TD
    subgraph Common["Common Failure Patterns Across All Sectors"]
        F1["Spend-based proxies\nmask high-intensity suppliers"]
        F2["Tier 2+ supply chain\nis effectively invisible"]
        F3["Downstream use phase\nis estimated, not measured"]
        F4["Allocation across multi-product\nprocesses is arbitrary"]
        F5["No financial incentive\nfor suppliers to improve\nor disclose"]
        F6["Annual measurement\ncannot track continuous\nsupply chain decisions"]
    end

    F1 & F2 & F3 & F4 & F5 & F6 --> Consequence["The Result:\n\nCompanies report Scope 3.\nThey do not manage it.\nThe market cannot price\nthe difference between\na leader and a laggard."]

    style Consequence fill:#e03131,color:#fff
```
