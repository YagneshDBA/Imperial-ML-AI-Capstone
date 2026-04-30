---
name: BBO Strategy Evolution
description: Week-by-week thinking and strategy decisions across 13 optimization rounds
type: project
---

# BBO Capstone — Strategy Evolution (Weeks 1-13)

## Strategic Phases

**Phase 1: Exploration (Weeks 1-3)**
- Pure exploration with high kappa UCB
- No function-specific knowledge
- Experimented with EI vs UCB (UCB won)
- Baseline data collection

**Phase 2: Pattern Discovery (Weeks 4-8)**
- Introduced local sampling around promising regions
- Manual intervention (Week 5) to fill sampling gaps
- Began moderate exploitation with mixed candidate pools
- Experimented with alternative kernels and LLM suggestions (Week 8) — GP+UCB remained strongest

**Phase 3: Function-Specific Optimization (Weeks 9-11)**
- Recognized each function requires different strategy
- Assigned explore/exploit/balanced modes per function
- Recovery adjustments when over-exploitation caused drops
- Clear performance separation emerged:
  - Strong: F5 (boundary), F7, F8 (converging)
  - Moderate: F2, F4, F6 (improving)
  - Weak: F1, F3 (stuck)

**Phase 4: Precision Refinement (Weeks 12-13)**
- **Week 12 Breakthrough**: Introduced multi-point local sampling (top-k best instead of single best)
  - F4 → first positive result
  - F6 → major improvement
  - F7, F8 → new bests
- **Week 13 Final**: Ultra-local exploitation
  - F5: Forced deterministic boundary `[0.999999]^4`
  - F7, F8: kappa<1.2, local_frac>0.70, multi-point sampling
  - F4, F6: Balanced refinement
  - F1, F3: Final exploration attempts

## Key Insights

**What worked:**
- Function-specific strategies over uniform approach
- Multi-point sampling (Week 12+) for mature functions
- Manual exploration (Week 5) to prevent sampling bias
- UCB outperformed EI for controllable exploration
- Recognizing boundary pattern in F5 and forcing it

**What was learned:**
- 1 query/week/function is extremely sample-starved for 4D+
- Some functions (F1, F3, F4, F6) likely have adversarial landscapes
- GP length_scale matters enormously (fixed 0.2 wasn't always optimal)
- Convergence detection is critical to shift from explore→exploit

**Why:** This evolution reflects learning the landscape structure iteratively. Early uniform strategies failed because functions have fundamentally different behaviors. Success came from adapting to observed patterns rather than forcing one methodology.

**How to apply:** When advising on optimization strategy, recognize:
- Current week number determines appropriate strategy phase
- Function performance history determines explore/exploit mode
- Multi-point sampling is only effective after Week 12 (sufficient data)
- Breakthrough weeks (5, 6, 12) came from strategic experimentation, not just parameter tuning
