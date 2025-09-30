# Outrank V4 - Gameflow Documentation

## Overview
Detailed documentation of the complete gameflow for Outrank V4.

---

## Game Setup

### Initial Setup
1. **Player Configuration**
   - Number of players: 2-4
   - Each player role: Human or AI

2. **Token Distribution**
   - Each player receives 2 hidden tokens
   - 6 tokens placed in center pool
   - Tokens belong to active category

3. **Blocking Chips**
   - Each player receives blocking chips
   - [Details TBD based on v4 changes]

---

## Round Flow

### 1. Challenge Phase
**Trigger**: Start of each round

**Actions**:
- Draw challenge card
- Display category and ranking criteria
- Reveal center pool (6 tokens)
- Players can see their hidden tokens

**Transition**: Automatically → Bidding Phase

---

### 2. Bidding Phase
**Trigger**: After challenge revealed

**Actions**:
- Players take turns bidding
- Bid = number of tokens they can correctly rank
- Players can pass
- Minimum bid: Must beat current high bid
- Maximum bid: Available tokens (hidden + visible center - blocked)

**Turn Order**:
- Clockwise from starting player
- Skip players who have passed

**End Condition**:
- All but one player has passed, OR
- All players pass (challenge skipped)

**Transition**: → Blocking Phase (if winner exists) OR → New Challenge (if all passed)

---

### 3. Blocking Phase
**Trigger**: Bidding complete with a winner

**Active Player**: All players except bid winner

**Actions**:
- Each player (except winner) can block center pool tokens
- Blocked tokens cannot be selected for ranking
- Constraint: Must leave enough tokens available for bid

**Validation**:
```
Available Tokens = Center Pool - Blocked + Winner's Hidden + Winner's Owned
Available Tokens >= Bid Amount
```

**Turn Order**:
- One turn per player (except winner)
- Clockwise from winner

**Transition**: → Ranking Phase

---

### 4. Ranking Phase
**Trigger**: Blocking complete

**Active Player**: Bid winner only

**Actions**:
1. **Token Selection**
   - Select exactly [bid amount] tokens
   - Sources: Center pool (not blocked), hidden tokens, owned tokens
   - Must all be from challenge category

2. **Ranking**
   - Arrange selected tokens in order
   - Order based on challenge criteria (e.g., highest → lowest GDP)
   - Drag-and-drop interface

3. **Submission**
   - Submit ranking for validation
   - Cannot change after submission

**Transition**: → Reveal Phase

---

### 5. Reveal Phase
**Trigger**: Ranking submitted

**Actions**:
1. **Validation**
   - Compare ranking against correct order
   - Show correct/incorrect positions
   - Animate reveal

2. **Result**
   - SUCCESS: All tokens correctly ranked
   - FAIL: Any token incorrectly ranked

**Transition**: → Scoring Phase

---

### 6. Scoring Phase
**Trigger**: Reveal complete

### If Ranking SUCCESS:
- **Bidder Gets**:
  - Points = bid amount
  - Ownership of ranked tokens
  - All blocking chips used against them

- **Blockers Get**:
  - No points
  - Lose their blocking chips (transferred to bidder)
  - No tokens

### If Ranking FAIL:
- **Bidder Gets**:
  - No points
  - No tokens
  - Loses ranked tokens (removed from game)

- **Blockers Get**:
  - Points = value of their blocking chip
  - Keep their blocking chips
  - Ownership of tokens they blocked

**Token Lifecycle**:
- Ranked tokens → Marked as used
- Blocked tokens (if fail) → Transfer to blocker
- Center pool → Refilled to 6 tokens
- Hidden tokens → Replaced if used

**Transition**: → Next Round (Challenge Phase) OR → Game End

---

## Game End

### Trigger
- [TBD - round limit? Token pool empty?]

### Final Scoring
- Base points from rounds
- End-game bonuses:
  - 1 point per remaining blocking chip
  - 1 point per owned token
  - [Any set collection bonuses TBD]

### Winner
- Player with highest total score

---

## State Management

### Game State Object
```javascript
gameState = {
    phase: 'setup|challenge|bidding|blocking|ranking|reveal|scoring',
    round: number,
    currentPlayer: index,
    players: array,

    // Challenge
    currentChallenge: object,
    currentCategory: string,

    // Tokens
    centerPool: array,
    tokenPools: object,
    usedTokenIds: set,

    // Bidding
    currentBid: number,
    highestBidder: index,
    passedPlayers: set,

    // Blocking
    blockedTokens: array,

    // Ranking
    selectedTokens: array,

    // Scoring
    scores: object,
    ownedTokens: object
}
```

---

## Notes

### Changes from V3
*To be documented as changes are implemented*

### Open Questions
*Design decisions still to be made*
