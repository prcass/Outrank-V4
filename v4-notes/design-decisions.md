# Outrank V4 - Design Decisions

## Purpose
This document records all design decisions made during v4 development, including alternatives considered and rationale for choices made.

---

## Decision Log

### [TEMPLATE - Copy for each decision]

**Decision #**: [Number]
**Date**: YYYY-MM-DD
**Topic**: [Brief topic name]

**Context**:
[What problem/question prompted this decision?]

**Options Considered**:
1. **Option A**: [Description]
   - Pros: [List]
   - Cons: [List]

2. **Option B**: [Description]
   - Pros: [List]
   - Cons: [List]

3. **Option C** (if applicable): [Description]
   - Pros: [List]
   - Cons: [List]

**Decision**:
[Which option was chosen]

**Rationale**:
[Why this option was selected over others]

**Impact**:
- Player Experience: [How it affects gameplay]
- Implementation: [Technical considerations]
- Balance: [Game balance implications]

**Implemented In**:
- Files: [List of modified files]
- Commit: [Git commit reference if applicable]

---

## Decisions Made

### Decision #1
**Date**: 2025-09-30
**Topic**: Replace Ranking with Draft & Guess Mechanic

**Context**:
V3 required players to perfectly rank multiple tokens in order, which was challenging and time-consuming. Need a more engaging, turn-by-turn mechanic that maintains tension and creates risk/reward decisions.

**Options Considered**:
1. **Keep V3 Ranking System**:
   - Pros: Already implemented, familiar
   - Cons: High difficulty, slow gameplay, limited player interaction during ranking phase

2. **Draft & Guess (Higher/Lower)**:
   - Pros: Turn-by-turn engagement, simple decision (higher/lower), continuous risk/reward, push-your-luck mechanic
   - Cons: Requires complete rewrite, less about perfect knowledge, more about calculated risks

3. **Auction/Bidding for Tokens**:
   - Pros: Economic strategy, resource management
   - Cons: Slower gameplay, less about trivia knowledge, favors players with more resources

**Decision**:
Draft & Guess (Higher/Lower) - Option 2

**Rationale**:
- Creates constant tension (risk all collected tokens each turn)
- Turn-by-turn keeps all players engaged
- Simpler decision (binary choice: higher/lower)
- Push-your-luck mechanic is exciting
- Faster gameplay than perfect ranking
- Still rewards trivia knowledge while adding risk management

**Impact**:
- Player Experience: More engaging, faster, risk/reward decisions each turn
- Implementation: Complete rewrite of core game loop (bidding, blocking, ranking phases all replaced)
- Balance: Luck vs. skill balance shifts toward calculated risk-taking

**Implemented In**:
- Files: TBD (outrank-v4-prototype.html)
- Commit: TBD

---

### Decision #2
**Date**: 2025-09-30
**Topic**: Risk Mechanic - Lose All Round Tokens on Wrong Guess

**Context**:
Need to create tension and risk in the push-your-luck mechanic. How much should players lose when they guess wrong?

**Options Considered**:
1. **Lose Only Drafted Token**:
   - Pros: Low punishment, encourages aggressive play
   - Cons: No real tension, minimal risk

2. **Lose All Tokens Collected This Round**:
   - Pros: High tension, meaningful risk/reward, encourages strategic cashing out
   - Cons: Can feel punishing, previous rounds' tokens are safe (complexity)

3. **Lose Entire Hand (All Rounds)**:
   - Pros: Maximum tension
   - Cons: Too punishing, discourages gameplay, would eliminate set collection strategy

**Decision**:
Lose All Tokens Collected This Round - Option 2

**Rationale**:
- Creates meaningful tension without being devastating
- Protects investment from previous rounds (encourages long-term strategy)
- Forces strategic decision: keep pushing or cash out?
- Maintains set collection as viable strategy across rounds

**Impact**:
- Player Experience: Exciting tension, strategic cashing out decisions
- Implementation: Need to track "round collected" vs "previous rounds" tokens
- Balance: Rewards both aggressive and conservative strategies

**Implemented In**:
- Files: TBD
- Commit: TBD

---

### Decision #3
**Date**: 2025-09-30
**Topic**: Hand Limit and Forced Actions

**Context**:
Without limits, players could hoard tokens indefinitely. Need to balance accumulation with strategic cashing out.

**Options Considered**:
1. **No Hand Limit**:
   - Pros: Simple, no forced actions
   - Cons: Optimal strategy = hoard until perfect sets, slows game

2. **8 Token Hand Limit with Forced Cash/Discard**:
   - Pros: Forces strategic decisions, prevents hoarding, maintains game pace
   - Cons: Additional complexity, can feel restrictive

3. **Lower Limit (5-6 tokens)**:
   - Pros: Forces frequent decisions
   - Cons: Too restrictive, limits set-building strategy

**Decision**:
8 Token Hand Limit with Forced Actions - Option 2

**Rationale**:
- 8 tokens = reasonable space for set building (can have 2 sets of 4, or 1 big + smaller sets)
- Forces periodic cashing out (maintains game flow)
- Creates interesting decisions when at limit
- Prevents "optimal hoarding" strategy

**Impact**:
- Player Experience: Meaningful decisions about when to cash out
- Implementation: Hand limit checking, force cash/discard UI
- Balance: Prevents runaway hoarding, maintains game pace

**Implemented In**:
- Files: TBD
- Commit: TBD

---

### Decision #4
**Date**: 2025-09-30
**Topic**: Set Scoring - One Token Per Set

**Context**:
Tokens have multiple tags (A1, B2, C3, D4). How should set scoring work?

**Options Considered**:
1. **Multiple Sets Per Token**:
   - Pros: Maximizes scoring potential, rewards finding overlaps
   - Cons: Complex scoring, optimal strategy unclear, hard to track

2. **One Token Per Set Only**:
   - Pros: Clear scoring, strategic choice (which set to use token for), simpler
   - Cons: Reduces scoring potential, tokens may feel "wasted"

**Decision**:
One Token Per Set - Option 2

**Rationale**:
- Clearer decision-making (which set do I want to complete?)
- Simpler scoring calculations
- Creates strategic tension (use token for 3-set or save for potential 4-set?)
- Easier to implement and explain

**Impact**:
- Player Experience: Clear strategic choices, easier to understand
- Implementation: Simpler scoring logic, clearer UI
- Balance: Forces prioritization decisions

**Implemented In**:
- Files: TBD
- Commit: TBD

---

### Decision #5
**Date**: 2025-09-30
**Topic**: Pool Size - 13 Tokens (1 Center + 12 Pool), Minimum 8 Refill

**Context**:
V3 used 6 center tokens + 2 hidden per player. V4 removes hidden tokens and bidding. How many tokens should be in play?

**Options Considered**:
1. **Small Pool (6-8 tokens)**:
   - Pros: Faster rounds, simpler
   - Cons: Limited choices, rounds end too quickly

2. **Medium Pool (12-13 tokens initially, min 8)**:
   - Pros: Good variety, rounds have substance, refill keeps game going
   - Cons: Moderate complexity

3. **Large Pool (20+ tokens)**:
   - Pros: Many choices, long rounds
   - Cons: Analysis paralysis, rounds drag, dilutes set collection

**Decision**:
Medium Pool (13 start, min 8 refill) - Option 2

**Rationale**:
- 12 draft choices = enough variety without overwhelming
- Minimum 8 refill = ensures subsequent rounds have substance
- Balances round length with decision quality
- Matches well with 8-token hand limit

**Impact**:
- Player Experience: Good variety each round, rounds have substance
- Implementation: Token pool management, refill logic
- Balance: Enough choices to be strategic, not so many to be overwhelming

**Implemented In**:
- Files: TBD
- Commit: TBD

---

## Deferred Decisions

### Game End Condition
**Status**: To be determined
**Options**:
- Round limit (e.g., 10 rounds)
- Score target (e.g., first to 30 points)
- Token depletion (pool can't be refilled to minimum 8)
- Time limit

**Next Step**: Playtest to determine which feels best

---

## Abandoned Ideas

### Bidding Phase
**Why Abandoned**: Draft & Guess mechanic makes bidding unnecessary. All players participate turn-by-turn instead of one winner attempting a challenge.

### Blocking Phase
**Why Abandoned**: No bidding = no blocking needed. Risk comes from guessing wrong, not from opponent interference.

### Hidden Tokens
**Why Abandoned**: Simplified V4 - all tokens visible in pool. Information is complete, decisions are about risk management not hidden information.

### Blocking Chips
**Why Abandoned**: No blocking phase means chips are unnecessary. Removed entirely from V4.
