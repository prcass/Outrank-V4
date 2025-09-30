# Outrank V3 → V4 Changelog

## Version 4.0 - [In Development]

### Overview
V4 represents a major gameplay overhaul, replacing the complex bidding/blocking/ranking system with a streamlined draft-and-guess push-your-luck mechanic. The core set collection goal remains, but the path to building sets is now faster, more engaging, and involves continuous risk/reward decisions.

---

## Major Gameflow Changes

### ❌ REMOVED: Bidding Phase
- **What Changed**: Completely removed bidding mechanic
- **Why**: Draft & guess creates turn-by-turn engagement without need for bidding
- **Impact**:
  - Game Rules: Entire bidding section removed
  - Code: All bidding logic removed
  - Player Experience: Faster gameplay, no waiting for auction to resolve
- **Status**: ✅ Designed
- **Date**: 2025-09-30

### ❌ REMOVED: Blocking Phase
- **What Changed**: Completely removed blocking and blocking chips
- **Why**: Risk now comes from guessing wrong, not opponent interference
- **Impact**:
  - Game Rules: Entire blocking section removed
  - Code: All blocking logic and chip tracking removed
  - Player Experience: Simpler, less downtime, more direct gameplay
- **Status**: ✅ Designed
- **Date**: 2025-09-30

### ❌ REMOVED: Hidden Tokens
- **What Changed**: No hidden tokens per player
- **Why**: Complete information simplifies game, decisions based on risk management not hidden knowledge
- **Impact**:
  - Game Rules: No hidden token distribution
  - Code: No per-player hidden token tracking
  - Player Experience: All tokens visible, decisions clearer
- **Status**: ✅ Designed
- **Date**: 2025-09-30

### ✅ NEW: Draft & Guess Mechanic
- **What Changed**: Players draft tokens and guess higher/lower vs center token
- **Why**: Creates engaging push-your-luck mechanic with constant tension
- **Impact**:
  - Game Rules: Complete new core gameplay loop
  - Code: New draft selection, comparison logic, risk mechanics
  - Player Experience: Fast, exciting, continuous engagement
- **Status**: 🔄 Designed, pending implementation
- **Date**: 2025-09-30

### ✅ NEW: Risk Mechanic (Lose Round Tokens)
- **What Changed**: Wrong guess = lose all tokens collected this round (not previous rounds)
- **Why**: Creates meaningful tension while preserving long-term strategy
- **Impact**:
  - Game Rules: New risk/reward section
  - Code: Track "this round" vs "previous rounds" tokens
  - Player Experience: Exciting decisions about when to stop pushing luck
- **Status**: 🔄 Designed, pending implementation
- **Date**: 2025-09-30

### ✅ NEW: Cash Out Mechanic
- **What Changed**: Players can cash out sets on their turn for immediate points
- **Why**: Creates strategic timing decisions and maintains game flow
- **Impact**:
  - Game Rules: New cash out rules and scoring
  - Code: Set detection, scoring logic, token retirement
  - Player Experience: Strategic decisions about when to cash vs. build bigger sets
- **Status**: 🔄 Designed, pending implementation
- **Date**: 2025-09-30

### ✅ NEW: Hand Limit (8 Tokens)
- **What Changed**: Maximum 8 tokens in hand, forced cash/discard if at limit
- **Why**: Prevents hoarding, maintains game pace
- **Impact**:
  - Game Rules: Hand limit rules
  - Code: Hand size validation, forced action UI
  - Player Experience: Forced periodic strategic decisions
- **Status**: 🔄 Designed, pending implementation
- **Date**: 2025-09-30

---

## Phase-by-Phase Changes

### Setup Phase
**V3**: 6 center tokens + 2 hidden per player + blocking chips
**V4**: 13 tokens total (1 center, 12 pool) + no chips
**Change**: Simplified setup, larger pool, no hidden tokens or chips

### Challenge Phase
**V3**: Challenge selected, tokens drawn
**V4**: Same - challenge selected, tokens drawn
**Change**: Pool size increased (13 vs 6+hidden)

### Bidding Phase
**V3**: Players bid on how many they can rank
**V4**: ❌ REMOVED
**Change**: Replaced with turn-by-turn draft & guess

### Blocking Phase
**V3**: Players place chips to block tokens
**V4**: ❌ REMOVED
**Change**: No blocking mechanic needed

### Ranking Phase
**V3**: Winner ranks all bid tokens perfectly
**V4**: ❌ REMOVED
**Change**: Replaced with simple higher/lower guess

### NEW: Draft & Guess Phase
**V3**: Did not exist
**V4**: Turn-by-turn draft token, guess higher/lower, collect or lose
**Change**: Core new mechanic

### Scoring Phase
**V3**: Points for successful ranking + set bonuses at game end
**V4**: Cash out sets anytime for immediate points, uncashed = 0 at game end
**Change**: Active cashing instead of passive end-game scoring

---

## Token Pool Management

### V3 Token Management:
- 6 center tokens
- 2 hidden per player
- Removed tokens replaced individually
- Blocking chips per player

### V4 Token Management:
- 13 tokens initial (1 center + 12 pool)
- All tokens visible
- Pool refilled to minimum 8 between rounds
- No chips

---

## Scoring Changes

### V3 Scoring:
- Ranking points: 1 per token ranked
- Blocking points: 2-6 per successful block
- End-game: Set bonuses (2-10 points) + 1 per owned token + 1 per remaining chip

### V4 Scoring:
**During Play:**
- **1 point per correct guess**: Immediate reward for each successful higher/lower call
- **1 bonus point**: Last player to pass in round
- **Cash out sets**: 2 tokens = 2pts, 3 tokens = 5pts, 4 tokens = 8pts (anytime on your turn)

**Turn Order:**
- **First Guesser privilege**: First player to pass OR guess wrong goes first next round

**Wrong Guess:**
- **Lose tokens** from this round (back to center pool)
- **Keep points** earned from correct guesses (KEY: separates points from tokens)

**End Game:**
- Only previously cashed points count
- Uncashed tokens = 0 points

---

## Set Collection Changes

### V3 Sets:
- Tokens collected passively (successful rankings, successful blocks)
- All sets scored at game end
- Multiple scoring paths

### V4 Sets:
- Tokens collected actively (correct guesses)
- Must cash out during game for points
- One token per set only
- Risk of losing uncashed tokens

---

## Breaking Changes
*Changes that make V4 incompatible with V3*

1. **No Blocking Chips**: Physical component removed entirely
2. **No Hidden Tokens**: Setup completely different
3. **Different Token Counts**: 13 vs 6+hidden distribution
4. **Core Mechanic**: Ranking replaced with draft & guess
5. **Scoring System**: Active cashing vs end-game bonuses
6. **Game State**: Must track "this round" vs "previous rounds" tokens

---

## Migration Notes
*V3 and V4 are fundamentally different games*

**Cannot directly convert V3 to V4** - requires complete reimplementation.

**Shared Elements**:
- Token design (tags around edges)
- Set collection goal
- Challenge system
- Turn-based structure

**New in V4**:
- Draft & guess mechanic
- Cash out system
- Hand limit
- Risk management

**Removed from V3**:
- Bidding
- Blocking
- Hidden tokens
- Chips
- Complex ranking

---

## Implementation Status

- ✅ Design complete
- ✅ Documentation updated
- ⏳ Prototype implementation pending
- ⏳ Testing pending
- ⏳ Rulebook update pending

---

## Next Steps

1. Update GAMEFLOW_V4.md with complete flow
2. Update GAME_RULES_V4.md with new rules
3. Implement in outrank-v4-prototype.html
4. Playtest and iterate
5. Determine game end condition
