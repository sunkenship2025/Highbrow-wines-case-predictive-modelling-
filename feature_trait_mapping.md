# Feature → Latent Trait Mapping Framework
## Highbrow Wines Predictive Model - Intuitive Analysis

---

## 🎯 Core Question
**Who buys premium wine online?**

Not just wine lovers. Not just digital shoppers.  
The intersection of: **Taste + Trust + Means + Motivation**

---

## 📋 The 6 Latent Behavioral Traits (FROZEN ONTOLOGY)

### 1. **Wine/Alcohol Affinity** (Gateway Trait)
### 2. **Culinary Sophistication** (Lifestyle Trait)  
### 3. **Digital Comfort** (Channel Enabler)
### 4. **Economic Freedom** (Capacity Trait)
### 5. **Customer Embeddedness** (Loyalty Signal)
### 6. **Life-Stage Context** (Constraint Layer)

**Critical Note:** These 6 traits are **FIXED** before modeling begins. No additional traits will be added during EDA or modeling phases.

**Occasionality/Event Signals:** These are NOT a 7th trait. They are **auxiliary contextual modifiers** folded into Culinary Sophistication. Occasionality is episodic and situational, not a stable latent characteristic.

---

## 🔍 TRAIT 1: Wine/Alcohol Affinity
**Question:** *"Are they already in the alcohol ecosystem?"*

### Why This Matters
You can't sell premium wine online to someone who doesn't drink wine.  
This is **necessary but not sufficient**.

### Strong Indicators (High Epistemic Confidence)
- `cat_Wijn_Stillewijnen_RAYON` → **Direct wine purchase history**
  - If they buy wine in-store, the category interest exists
  - But offline ≠ online willingness
  
- `cat_AP_STDR_PortoONLINE` → **Premium fortified wine, ONLINE**
  - This is GOLD: premium alcohol + digital channel + specialty taste
  - Signals: "I trust buying premium alcohol remotely"
  
- `cat_AP_STDR_WhiskyONLINE` → **High-end spirits, ONLINE**
  - Similar logic to Porto
  - Shows comfort with expensive, non-returnable purchases online

### Moderate Indicators (Medium Epistemic Confidence)
- `cat_Bier_Genietbieren` → **Craft/specialty beer**
  - Signals appreciation for quality over mass market
  - But beer drinkers ≠ wine drinkers necessarily
  - Still, shows "enthusiast" mindset

**⚠️ Important:** Confidence levels represent my prior beliefs about how strongly features signal traits. These are NOT feature weights or model coefficients. The model will determine actual predictive power empirically.

### Critical Insight
**Wine buying offline does NOT predict wine buying online.**  
Many loyal wine shop customers are digital laggards.

The *ONLINE* alcohol purchases are far more predictive than offline wine history.

---

## 🍽️ TRAIT 2: Culinary Sophistication
**Question:** *"Do they see food/drink as experience, not just fuel?"*

### Why This Is The Secret Weapon
Premium wine is a **lifestyle complement**, not a standalone product.  
Highbrow wine buyers are already living a certain way.

### Tier 1: Gourmet Proteins (High Epistemic Confidence)
These are **choice signals** — you don't accidentally buy these:

- `cat_Tapas` → Experiential, social, Mediterranean luxury
- `cat_VisGerookt` → Smoked fish (not fish sticks)
- `cat_VNCWildSteak` → Game meat, adventurous palate
- `cat_VNCLamSnedenkoteletsteak` → Premium lamb cuts
- `cat_VNCKalfStoofvlees` → Veal stew (high-end comfort)
- `cat_VNCCharBHWildpasteien` → Wild game terrines (niche, gourmet)

**If someone buys wild boar pâté, they're not a "grab a bottle of red" person.**

### Tier 2: Artisan Dairy & Seasonal (High Epistemic Confidence)
- `cat_KaasSeizoenskazen` → **Seasonal specialty cheese**
  - Not cheddar. Not gouda in plastic.
  - This is "pairing cheese" — bought WITH wine mindset
  
- `cat_VerseKaasFruitkazen` → Fruit cheeses (gourmet overlap)

### Tier 3: Convenience-With-Quality (Medium Epistemic Confidence)
- `cat_Ber_Ger_VersMaaltijdsalades` → Fresh prepared salads
- `cat_Ber_Ger_DVPortioneerbaar` → Portioned deli items
- `cat_VNCBGBereidegerechten` → Prepared meat dishes

**Interpretation:** Time-poor but quality-conscious.  
Won't sacrifice taste for speed. Will pay for preparation.

### Tier 4: Event/Occasionality Signals (Low Epistemic Confidence - Auxiliary Only)
These are **NOT core trait indicators**—they are contextual modifiers:

- `cat_Bloemen` → Flowers (occasions, hosting)
- `cat_bbqfoodevent` → BBQ event products  
- `cat_nfokay` → Catch-all category

**Why folded into this trait:**  
Occasionality is **episodic, not latent**. Someone buying wine + flowers + tapas is likely hosting, which provides *context* for culinary sophistication, but isn't a stable behavioral trait. These features may help identify trigger events for trial, but should not be interpreted as primary drivers.

### The Negative Space (What They DON'T Buy)
- `cat_Chips` → Impulse, low-margin, mass-market
  - If this is a TOP feature, something's wrong
  - Small amounts OK, but not a lifestyle marker

---

## 💻 TRAIT 3: Digital Comfort
**Question:** *"Will they buy wine (risky, sensory) online?"*

### Why This Trumps Wine Knowledge
**Insight:** More wine lovers are offline than you think.  
The 55+ demographic knows wine but fears e-commerce.

### Tier 1: Proven Online Shoppers (High Epistemic Confidence)
- `Collishop_customer` → **THE GOLDEN FEATURE**
  - They've crossed the psychological barrier
  - They trust delivery, digital payment, perishable logistics
  - If you've bought groceries online, wine is a smaller leap

### Tier 2: Hybrid Channel Users (Medium Epistemic Confidence)
- `n_cogo` → Number of "collect & go" orders
- `cogo_rev` → Revenue via collect & go
  
**Why this matters:** Click & collect is the **bridge behavior**.  
- Digital ordering (tech comfort)
- Physical pickup (control retained)
- This person is 70% ready for full online

### Tier 3: Tech Adjacency (Medium Epistemic Confidence)
- `cat_ColruytMobile_Toestellen` → Mobile device purchases
  - Not causative, but correlative
  - Comfortable buying electronics = tech-savvy

### The Digital Divide
Age and digital comfort are **not the same**.  
- A 60-year-old Collishop user > a 30-year-old who only shops in-store
- Behavior > Demographics

---

## 💰 TRAIT 4: Economic Freedom
**Question:** *"Can they afford €20-40 bottles regularly?"*

### Why Price Sensitivity Matters More Than Income
We don't have income data.  
We have **revealed preferences through spending patterns**.

### Direct Economic Signals (High Epistemic Confidence)
- `price_sens_colr` → **Price sensitivity score**
  - Expected direction: NEGATIVE correlation
  - Less price-sensitive → more likely to buy premium
  
- `rev_ticket` → **Average basket value**
  - Higher ticket → economic capacity
  - But also: shopping habits (bulk vs. frequent)
  
- `prod_ticket` → **Products per basket**
  - Basket composition insight
  - More products = different shopping style

### Indirect Economic Signals (Medium Epistemic Confidence)
- `total_discount` → **Total discount usage**
  - Expected: NEGATIVE correlation
  - Heavy discount users unlikely to buy full-price premium wine
  - But: Smart shoppers also use discounts strategically

### The Nuance
**High spending ≠ high income always**  
Could be:
- Large families (necessity)
- Party shoppers (occasional)
- Premium lifestyle (our target)

Need to look at **WHAT** they spend on, not just how much.

---

## 🤝 TRAIT 5: Customer Embeddedness
**Question:** *"How deep is their relationship with Colruyt?"*

### Why This Is Non-Linear

**Hypothesis:** The relationship is **CURVILINEAR** (inverted U-shape)

- **Very Low SOW** → Occasional, not engaged, won't try new things
- **Medium-High SOW** → **Sweet spot** — trust + openness
- **Very High SOW** → Routine, habit-driven, risk-averse

### The Features
- `SOW_colr` → Share of wallet (continuous)
- `SOW_type_colr` → Segmented buckets

### Expected Pattern
| SOW Segment | Conversion Rate | Why |
|-------------|----------------|-----|
| 0-20% | Low | Not engaged enough |
| 30-60% | **High** | Trust + openness |
| 70-90% | Medium | Established habits |
| 90-100% | Low | Ultra-routine, no exploration |

### The Psychological Insight
**Outlier_fr** customers (100%+ SOW) might be:
- Budget-constrained (Colruyt for price)
- Geographically isolated
- Habit-locked

Not necessarily premium product seekers.

---

## 👨‍👩‍👧‍👦 TRAIT 6: Life-Stage Context
**Question:** *"What life constraints reduce discretionary luxury?"*

### Why This Is Weak But Necessary
These features rarely **cause** wine buying.  
But they **constrain** it.

### Active Parenting Stage (Low Epistemic Confidence - Contextual)
- `cat_Babyluiers` → Diapers (young children)
- `cat_Zomerspeelgoed` → Summer toys

**Interpretation:**  
Time-starved, budget-redirected to kids.  
Less mental space for "wine discovery."

### Elder Care Stage (Low Epistemic Confidence - Contextual)
- `cat_Incontinentie_luiers` → Incontinence products

**Interpretation:**  
Caregiver burden, different priorities.

### Household Maintenance (Low Epistemic Confidence - Contextual)
- `cat_Textiel_Bedlinnen` → Bedding
- `cat_Textiel_Herenondergoed` → Men's underwear
- `cat_Textiel_Pantys` → Pantyhose

**Interpretation:**  
Routine household provisioning.  
Not lifestyle shoppers.

### The Household Typology Variable
- `HOUSEHOLDTYPOLOGY` → Structured life-stage segments

**Use case:** Interaction terms only.  
Example: *Tapas × HH_nochild_55+ might be powerful*

### Life-Stage Hypothesis
| Segment | Expected Behavior |
|---------|------------------|
| Singles 35-54 | High exploration, disposable income |
| Couples no kids 55+ | **PRIME TARGET** — time, money, taste |
| Young families | Low (constrained) |
| Teens at home | Medium (entertaining, dinners) |
| Empty nesters | High (rediscovering leisure) |

---

## ✅ The "Would It Make Sense?" Test

### If This Feature Was #1 in Feature Importance, Would I Believe It?

| Feature                       | Believable? | Why / Why Not          |
|--------------------------------|-------------|------------------------|
| `Collishop_customer`            | ✅ YES | Digital trust is the barrier |
| `cat_Tapas`                     | ✅ YES | Lifestyle marker |
| `price_sens_colr`               | ✅ YES | Economic freedom |
| `cat_Wijn_Stillewijnen_RAYON`   | ✅ YES | Category affinity |
| `cat_AP_STDR_PortoONLINE`       | ✅ YES | Both traits combined |
| `SOW_colr`                      | ⚠️ MAYBE | Non-linear, needs investigation |
| `rev_ticket`                    | ✅ YES | Spending capacity |
| `cat_Babyluiers`                 | ❌ NO | Constraint, not driver |
| `cat_Chips`                      | ❌ NO | Wrong lifestyle |
| `cat_Bloemen`                     | ❌ NO | Too occasional |
| `HOUSEHOLDTYPOLOGY`              | ⚠️ DEPENDS | Only via interactions |

---

## 🚨 Red Flags to Watch For

### If The Model Shows These, Investigate:
1. **Household maintenance products ranked high**  
   → Likely spurious correlation or data leakage
   
2. **Very high SOW = best predictor**  
   → Missing the non-linear relationship
   
3. **Age/demo features dominate**  
   → Behavior > demographics always
   
4. **Offline wine > online alcohol**  
   → Channel matters more than category
   
5. **No interaction terms matter**  
   → Real behavior is multiplicative, not additive

---

## 🧪 Expected Top 10 Features (My Hypothesis)

### Ranked by Intuition:

1. **`Collishop_customer`** — Proves digital trust
2. **`cat_AP_STDR_PortoONLINE`** — Premium + online + alcohol
3. **`price_sens_colr` (negative coef)** — Economic freedom
4. **`cat_Tapas`** — Lifestyle/culinary sophistication
5. **`cat_Wijn_Stillewijnen_RAYON`** — Category familiarity
6. **`cogo_rev`** — Hybrid digital behavior
7. **`cat_KaasSeizoenskazen`** — Gourmet pairing mindset
8. **`rev_ticket`** — Spending capacity
9. **`cat_VisGerookt`** — Sophisticated palate
10. **`SOW_colr` (non-linear term)** — Engagement sweet spot

---

## 🎯 Feature Engineering Hypotheses (NOT for Immediate Implementation)

**⚠️ CRITICAL:** These are **hypotheses to be tested AFTER baseline modeling**, not features to build now.

### Why Not Build These Yet?

1. **Avoid baking in assumptions** — Let the model discover patterns first
2. **Preserve interpretability** — Raw features allow falsification of hypotheses  
3. **Prevent premature optimization** — Composite scores may not improve over raw features
4. **Enable learning** — Model feature importance will tell us if these structures exist

### Sequencing Rule:
```
1. Train baseline with RAW features
2. Analyze feature importance  
3. Check if model implicitly learns these patterns
4. ONLY THEN consider composites if signal is fragmented
```

---

### Hypothesized Composite Scores (For Post-Baseline Consideration)

**IF baseline shows fragmented signal across related features, THEN consider:**

1. **Culinary Sophistication Index** (Hypothesis)
   - Aggregate gourmet protein + specialty cheese + smoked fish features
   - *Test: Does this improve over individual features?*

2. **Digital Readiness Score** (Hypothesis)
   - Combine Collishop binary + COGO usage + mobile purchases
   - *Test: Or is Collishop alone sufficient?*

3. **Economic Freedom Score** (Hypothesis)
   - Combine basket value + price sensitivity + discount usage
   - *Test: Do these load on same latent factor?*

4. **Alcohol Engagement Score** (Hypothesis)
   - Combine wine offline + online premium spirits + craft beer
   - *Test: Or do offline/online split matter more?*

---

### Hypothesized Interaction Terms (For Post-Baseline Testing)

**IF main effects are significant, THEN test these interactions:**

- **Culinary × Digital** → `Tapas × Collishop`  
  *Hypothesis: Gourmet + online trust = multiplicative effect*

- **Alcohol × Digital** → `Wine_offline × Collishop`  
  *Hypothesis: Wine lovers who cross digital barrier convert highest*

- **Life-stage × Premium** → `HH_type × Tapas`  
  *Hypothesis: Empty nesters + gourmet = segment interaction*

- **SOW Quadratic** → `SOW + SOW²`  
  *Hypothesis: Capture inverted-U relationship*

**Current Status:** These remain **untested hypotheses**. Model results may confirm, reject, or refine them.

---

## 🎓 Key Insights Summary

### What Drives Highbrow Wine Online Purchase?

**It's NOT:**
- Just loving wine (many wine lovers shop offline)
- Just being digital-savvy (buy groceries ≠ buy wine)
- Just having money (rich ≠ premium taste)

**It's THE INTERSECTION:**
```
Premium Wine Buyer = 
    Culinary Sophistication
    × Digital Trust
    × Economic Freedom
    × (Category Interest)
    × (1 - Life Constraints)
```

### The Archetypes:

1. **"The Connected Gourmet"** ⭐ (Best Target)
   - Buys Tapas, seasonal cheese, game meat
   - Active Collishop user
   - Medium-high SOW (50-70%)
   - 45-65 years old, no young kids
   - Low price sensitivity

2. **"The Digital Wine Lover"** ⭐
   - Buys wine offline regularly
   - Already buys Porto/Whisky online
   - Comfortable with COGO
   - Just needs the nudge

3. **"The Aspirational Explorer"**
   - Younger (35-45)
   - High digital comfort
   - Medium culinary sophistication
   - Price-conscious but willing to splurge

4. **"The Offline Traditionalist"** ❌ (Hard Sell)
   - Loves wine
   - Never uses Collishop
   - 60+, set in ways
   - Won't convert easily

---

## 📊 Validation Checks

### After Model Training, Ask:

1. **Do the top features make intuitive sense?**
2. **Are interactions present?** (Real behavior is multiplicative)
3. **Is SOW relationship non-linear?** (Should be inverted-U)
4. **Do life-stage variables matter only in context?**
5. **Does digital channel behavior beat offline category behavior?**

### If Any Of These Fail:
- Feature engineering needed
- Non-linear terms missing
- Possible data leakage
- Wrong model class (try tree-based, not linear)

---

## 🏁 Final Thought

**Buying premium wine online is an act of trust + taste + means.**

The model should capture:
- **Taste** → Culinary sophistication features
- **Trust** → Digital behavior features
- **Means** → Economic freedom features

Everything else is context or noise.

---

*This mapping reflects intuitive understanding BEFORE any modeling or EDA-1.*  
*All confidence levels are epistemic priors, not model weights.*  
*All composite scores are hypotheses to test, not features to build immediately.*  
*Compare baseline model results to these hypotheses to validate or challenge assumptions.*
